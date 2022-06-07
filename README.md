# XQUERY-1stProject
    A partir del archivo enunciado.xml, accede a los siguientes elementos:
    
####  Ejercicio 1. Muestra todos los títulos de los artículos de pubmed ordenado por el título.
        for $Title in //PubmedArticle
        order by $Title//ArticleTitle
        return $Title//ArticleTitle

####  Ejercicio 2. Muestra todos los nombres de las sustancias químicas que se encuentra en cada artículo ordenado por el atributo UI.
        for $subs in //Chemical
        order by $subs/NameOfSubstance/@UI
        return $subs/NameOfSubstance

####  Ejercicio 3. Muestra todos los nombres de las sustancias químicas que se encuentra en cada artículo ordenado por el atributo UI. Pero ahora, sólo hay que ver los nombres que comienzan por la letra "C".
        for $c in //Chemical
        where starts-with($c/NameOfSubstance,'C')
        order by $c/NameOfSubstance/@UI
        return $c/NameOfSubstance


####  Ejercicio 4. Calcula cuántos autores tenemos en total.
        for $aut in /PubmedArticleSet
        return count($aut//Author)
        

####  Ejercicio 5. Contenga cuántos autores tenemos en cada artículo.
        for $aut in //PubmedArticle
        return ($aut//ArticleTitle,count($aut//Author))

####  Ejercicio 6. Muestre el título de los artículos que tienen más de 2 autores.
        for $tit in //Article
        where count($tit//Author)>2
        return $tit//ArticleTitle


####  Ejercicio 7. Muestra la media aritmética de DateCompleted y DateRevised. Hazlo los dos en la vez.
        let $avgrevised := avg(for $c in //DateRevised
        return $c/Year)
        let $avgcompleted := avg(for $c in //DateCompleted
        return $c/Year)
        return concat("AVG REVISED:",$avgrevised," AVG COMPLETED:",$avgcompleted)


####  Ejercicio 8. Muestra la media aritmética de las dos medias anteriores. Utilice el código del apartado anterior (no los números resultantes).
        let $avgrevised := avg(for $c in //DateRevised
        return $c/Year)
        let $avgcompleted := avg(for $c in //DateCompleted
        return $c/Year)
        return ($avgrevised+$avgcompleted) div 2


####  Ejercicio 9. Muestra los países diferentes que salen por cada artículo de pubmed
        for $art at $n in //PubmedArticle
        return (concat("Paissos diferents del Article ",$n," (",$art//ArticleTitle,"):"),distinctvalues($art//Country))


####  Ejercicio 10. Ocurre en HTML el ejercicio 1, en formato de lista ordenada.
        <ol>
        {
        for $Title in //PubmedArticle
        order by $Title//ArticleTitle
        return <li>{data($Title//ArticleTitle)}</li>
        }
        </ol>

####  Ejercicio 11. Ocurre en HTML el ejercicio 2, en formato de lista ordenada.
        for $x in /*
        return <table><tr><th>{"Name of Substance"}</th></tr>
        {
        for $subs in //Chemical
        order by $subs/NameOfSubstance/@UI
        return <tr><td>{data($subs/NameOfSubstance)}</td></tr>
        }
        </table>

####  Ejercicio 12. Ocurre en HTML el ejercicio 5, en formato de lista ordenada.
        for $x in /*
        return <table><tr><th>{"Article Title"}</th><th>{"Total of authors"}</th></tr>
        {
        for $aut in //PubmedArticle
        return <tr><td>{data($aut//ArticleTitle)}</td><td>{count($aut//Author)}</td></tr>
        }
        </table>
