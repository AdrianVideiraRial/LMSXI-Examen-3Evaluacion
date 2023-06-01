### Examen 3 evaluacion

- Realiza las siguientes consultas en xquery con el fichero premios.xml (repositorio):
        1. (1 punto) Devuelve la frase "[nombre] ha ganado el premio de [categoria] en el año [año]"

        for $x in doc("premios.xml")/premios_nobel/premios/premio
        let $nombre := ($x/premiado)
        let $categoria := ($x/@categoria)
        let $año := ($x/año)
        return concat($nombre, "ha ganado el premio de ", $categoria, " en el año ",$año)

        2. (1 punto) Una tabla html [categoria] | [premiado] ordenada de mayor a menor por los [años]

        <ul>
            {
                for $x in doc("premios.xml")/premios_nobel/premios/premio
                order by ($x/año)
                return
                <premiado>
                <categoria>{data($x/@categoria)}</categoria>
                <premiado>{data($x/premiado)}</premiado>
                </premiado>
            }
        </ul>

        3. (2 punto) Incluir un nuevo premiado en un nuevo fichero
   
            let $premios := doc("C:\Users\VidE\Desktop\DAW\LMSXI\Examen 3 Evaluacion\premios.xml")/premios_nobel/premios/premio
            let $nuevo_premiado := <premio categoria ="Bioquimica">
                           <año>1993</año>
                           <premiado>Kary Mullis</premiado>
                           <motivo>Descubrimiento reaccion en cadena de la polimerasa</motivo>                  
                       </premio>
            let $nuevoDocumento := <premios_nobel>
                           <premios>
                               <premio>{$premios/alumno, $nuevo_premiado}</premio>
                           </premios>
                       </premios_nobel>
            return $nuevoDocumento


        4. (2 puntos) Realizar un fichero nuevo incluyendo motivos en los que no tienen

            let $premios := doc("premios.xml")/premios_nobel/premios/premio

            let $premios_con_motivo :=
            for $premio in $premios
            let $motivo := $premio/motivo
            return
                if (exists($motivo))
                then $premio
                    else
                    <premio categoria="{data($premio/@categoria)}">
                        {$premio/año}
                        {$premio/premiado}
            <motivo>Sin motivo especificado</motivo>
            </premio>

            let $nuevoDocumento :=
            <premios_nobel>
                <premios>{$premios_con_motivo}</premios>
            </premios_nobel>

            return $nuevoDocumento


- Realiza una aplicación para usar el fichero employees.json (repositorio)
- 
        1. (2 puntos) Que lea el fichero y guarde los datos en un array list

        2. (2 puntos) Despues de modificar algun datos en el array list que lo vuelva a guardar

