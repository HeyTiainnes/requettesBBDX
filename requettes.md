--1. Liste des potions : Numéro, libellé, formule et constituant principal. (5 lignes)
select p.num_potion ,p.lib_potion ,p.formule , p.constituant_principal  from potion p;
--2. Liste des noms des trophées rapportant 3 points. (2 lignes)
select c.nom_categ from categorie c where c.nb_points = 3;
--3. Liste des villages (noms) contenant plus de 35 huttes. (4 lignes)
select v.nom_village from village v where nb_huttes >35;
--4. Liste des trophées (numéros) pris en mai / juin 52. (4 lignes)
select t.num_trophee, t.date_prise 
from trophee t
where t.date_prise 
between '2052-05-01' and '2052-06-30'; 
--5. Noms des habitants commençant par 'a' et contenant la lettre 'r'. (3 lignes)
select h.nom from habitant h where h.nom like 'A%'and h.nom like '%r%';
--6. Numéros des habitants ayant bu les potions numéros 1, 3 ou 4. (8 lignes)
----
--7. Liste des trophées : numéro, date de prise, nom de la catégorie et nom du preneur. (10lignes)
select t.num_trophee, date_prise, code_cat, num_preneur  from trophee t ; 
--8. Nom des habitants qui habitent à Aquilona. (7 lignes)
select h.nom  from habitant h 
join village v on v.num_village = h.num_village 
where v.nom_village ='Aquilona';

--9. Nom des habitants ayant pris des trophées de catégorie Bouclier de Légat. (2 lignes)
select h.nom from habitant h
join trophee t on t.num_preneur  = h.num_hab 
join categorie c on c.code_cat = t.code_cat    
where c.nom_categ = 'Bouclier de Légat';

--10. Liste des potions (libellés) fabriquées par Panoramix : libellé, formule et constituantprincipal. (3 lignes)
select lib_potion, formule, constituant_principal  
from potion p
join fabriquer f on p.num_potion = f.num_potion 
join habitant h  on h.num_hab = f.num_hab
where h.nom = 'Panoramix';

--11. Liste des potions (libellés) absorbées par Homéopatix. (2 lignes)
select distinct lib_potion from potion p 
join absorber a  on p.num_potion  = a.num_potion
join habitant h on h.num_hab = a.num_hab 
where h.nom = 'Homéopatix';

--12. Liste des habitants (noms) ayant absorbé une potion fabriquée par l'habitant numéro 3. (4 lignes)

select distinct h.nom from habitant h
join absorber a on a.num_hab = h.num_hab  
join potion p on p.num_potion = a.num_potion 
join fabriquer f on f.num_potion = p.num_potion 
join habitant h2 on h2.num_hab = f.num_hab 
where f.num_potion = 3;
--select distinc h.nom from habitant h 



--13. Liste des habitants (noms) ayant absorbé une potion fabriquée par Amnésix. (7 lignes)
--select h.nom  from habitant h  
--join fabriquer f from h.num_ = f.num_hab 
--join potion p from p.num_potion = h.nom 
--where h.nom ='Amnésix';

--select h.nom from habitant h
--join fabriquer f on f.num_hab = h.num_hab 
--join potion p on f.num_potion = p.num_potion 
--join absorber a on a.num_potion = a.num_hab 
--where h.nom  = 'Amnésix' ;

select distinct h.nom from habitant h 
join absorber a on a.num_hab = h.num_hab 
join potion p on p.num_potion = a.num_potion
join fabriquer f on f.num_potion = p.num_potion 
join habitant h2 on f.num_hab = h2.num_hab 
where h.nom ='Amnésix';


--14. Nom des habitants dont la qualité n'est pas renseignée. (2 lignes)
select h.nom from habitant h 
where h.num_qualite is null ;


--15. Nom des habitants ayant consommé la Potion magique n°1 (c'est le libellé de lapotion) en février 52. (3 lignes)
select h.nom from habitant h 
join absorber a on a.num_hab = h.num_hab 
where a.num_potion = 1 and a.date_a 
between '2052-02-18' and '2052-02-20';


--16. Nom et âge des habitants par ordre alphabétique. (22 lignes)
select h.nom, h.age from habitant h 
order by h.nom ;


--17. Liste des resserres classées de la plus grande à la plus petite : nom de resserre et nom du village. (3 lignes)
select r.nom_resserre, v.nom_village from resserre r 
join village v ON r.num_village = v.num_village 
order by r.superficie  desc ;



--***v

--18. Nombre d'habitants du village numéro 5. (4)

select count(h.num_village)  from habitant h 
where num_village =(5);

--19. Nombre de points gagnés par Goudurix. (5)
select sum(c.nb_points)  from categorie c
join trophee t on t.code_cat = c.code_cat 
join habitant h on t.num_preneur = h.num_hab 
where h.nom = 'Goudurix';


--20. Date de première prise de trophée. (03/04/52)
select MIN(date_prise)  from trophee t ;


--21. Nombre de louches de Potion magique n°2 (c'est le libellé de la potion) absorbées. (19)

select sum(a.quantite) from absorber a
join potion p on a.num_potion = p.num_potion 
where p.lib_potion = 'Potion magique n°2';

--22. Superficie la plus grande. (895)

select MAX(r.superficie)  from resserre r ;

--***

--23. Nombre d'habitants par village (nom du village, nombre). (7 lignes)

-- compter le nombre d'occurences identiques : sum
-- tbl habitants : cln numero de village.
-- tbl village : cln nom village
--> selectionner dans la table habitant le numero les numero de village
	--> additionner les numeros identiques (nombre occurences)
-- > lier les numero de village aux nom de villages (table villages)




select v.nom_village, h.num_hab  
from habitant h, village v2  
join village v  
on h.num_village = v.num_village
group by v.num_village  ;



--- *****
--- *****

--****SELECT Age, count(*) AS "Nombre d'employés"  FROM Employes GROUP BY Age;****
--
--SELECT colonne1, colonne2, ... colonneN,   
--fonction_agregation (nom_colonne)  
--FROM tables  
--[WHERE conditions]  
--GROUP BY colonne1, colonne2, ... colonneN;


--24. Nombre de trophées par habitant (6 lignes)

--25. Moyenne d'âge des habitants par province (nom de province, calcul). (3 lignes)

--26. Nombre de potions différentes absorbées par chaque habitant (nom et nombre). (9lignes)


--27. Nom des habitants ayant bu plus de 2 louches de potion zen. (1 ligne)


--***
--28. Noms des villages dans lesquels on trouve une resserre (3 lignes)

--29. Nom du village contenant le plus grand nombre de huttes. (Gergovie)

--30. Noms des habitants ayant pris plus de trophées qu'Obélix (3 lignes).


