El torneo está compuesto por 20 equipos. 
Es un torneo de ida y vuelta (todos juegan todos), 
por lo que tiene 19 rondas, 
y cada equipo juega una vez por ronda. 
Cada equipo se enfrenta a los demás una vez en el torneo (cada partido no se repite en el torneo).
Tu misión es implementar una función ""buildMatchesTable"" que reciba el número de equipos 
(siempre un número positivo y par) 
y devuelva una matriz

```
[
  [[1,2], [3, 4]], // primera ronda: 1 vs 2, 3 vs 4
  [[1,3], [2, 4]], // segunda ronda: 1 vs 3, 2 vs 4
  [[1,4], [2, 3]]   // tercera ronda: 1 vs 4, 2 vs 3
]
```

No debería importarte el orden de los equipos en el partido, 
ni el orden de los partidos en la ronda. 
Sólo deberían importarte las reglas del torneo


```php

function buildMatches($numero){
    $aFixtures = [];
    $crucesxEquipo = [];
    $paso = 1;
    for($i=1;$i<$numero;$i++){// numero de jorndas
        $fixturexJornada = [];
        $equiposEstaJornada = [];
        for($j=1; $j<=$numero; $j++){// numero de equipos
            if(count($fixturexJornada) >= intval($numero / 2)){
                break;
            }
            if(in_array($j, $equiposEstaJornada)){
               continue;
            }
            if(!isset($crucesxEquipo[$j])){
                $crucesxEquipo[$j] = [];
            }
            $equipoActual = validarNoMayoraNumero($j + $paso, $numero, $equiposEstaJornada, $j);
            if($equipoActual!==$j && !in_array($equipoActual, $crucesxEquipo[$j])){
                $crucesxEquipo[$j][] = $equipoActual;
                $fixturexJornada[] = [$j, $equipoActual];
                $equiposEstaJornada[] = $j;
                $equiposEstaJornada[] = $equipoActual;
            }
        }
        $paso++;
        $aFixtures[] = $fixturexJornada;
    }
    return $aFixtures;
}

function validarNoMayoraNumero($equipoActual, $numero, $equiposEstaJornada, $retador){
    $nuevoEquipoActual = $equipoActual;
    if($equipoActual>$numero){
        $nuevoEquipoActual = $equipoActual - $numero;    
    }
    if(in_array($nuevoEquipoActual, $equiposEstaJornada)){
        for($i=1; $i<=$numero; $i++){
            if($i === $retador){
                continue;
            }
            if(!in_array($i, $equiposEstaJornada)){
                $nuevoEquipoActual = $i;
                break;
            }
        }
    }
    return $nuevoEquipoActual;
}

var_dump(buildMatches(6));

```
