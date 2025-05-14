

# Ejemplo 1
1. 
$$ \{ <b, c> | \: <a,b,c,d> \: \in Pelicula  \} $$
Tambien se usa sin comas entre las variables de dominio

2. 
$$ \{ <b> | <abcd> \: \in Pelicula \land \text{d = 'Steven Spielberg'}  \} $$

3. 
$$ \{ <bcf> | <abcd> \: \in Pelicula \land (\exists \:eg) (<efg> \: \in Puntuacion \land  a = e \land g = 5) \:  \} $$


# Ejemplo 2

- Estudiante 
	- CodEst: a
	- Nombre: b
	- Especialidad: c
- Curso
	- Dept: d
	- Num: e
	- Titulo: f
- Departamento
	- Abrev: g
	- Nombre: h
	- Oficina: i
- Matricula
	- IdEstud: j
	- Dept: k
	- Num: l
	- Fecha: m

1. 
$$ \{ <gf> | (\exists \: g)<ghi> \: \in Departamento \: \land (\exists de)(<def> \: \in Curso \: \land \: d = g \: \land \: e = 101)  \} $$

2. 
$$ \{ <ba> |(\exists \: c) <abc> \: \in Estudiante \: \land \: c = 'CC' \: \} $$

3. 
$$ \{ <i> | (\exists  g) <ghi> \: \in Depart \land (\exists \: de)(<def> \in Curso \: \land \: d = g \: \land \: \text{d = 'cm'} \: \land \: e = 243) \} $$


4. 
$$ \{ <f> | (\exists ) <def> \in Curso \land (\exists kl)(<jklm> \in Matricula  \land d = k \land e = l $$
$$  \land (\exists gh )(<ghi> \in Departamento \land g = k \land h = 'Quimica' )) \} $$
