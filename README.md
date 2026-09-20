# 20-ejercicios-python
Ejercicios de python
#1 Validador de notas con promedio
#Clase Calificador que: (1) tenga método validar_nota(nota) que retorne True si 0 ≤ nota ≤ 100, False en caso contrario; (2) tenga método cargar_notas(*args) que reciba múltiples notas, las valide, agregue solo las válidas a una lista interna, y retorne esa lista; (3) tenga método promedio() que retorne el promedio de notas almacenadas.
class Calificador:
    def __init__(self):
        self.notas = []

    def validar_nota(self, nota):
        return 0 <= nota <= 100

    def cargar_notas(self, *args):
        for nota in args:
            if self.validar_nota(nota):
                self.notas.append(nota)
        return self.notas

    def promedio(self):
        if not self.notas:
            return 0
        return sum(self.notas) / len(self.notas)


c = Calificador()
print(c.cargar_notas(85, 92, 110, 78, -5, 88))
print(c.promedio())

# 2 Contador de palabras únicas
# Clase AnalizadorTexto que: (1) tenga método agregar_palabra(palabra) que agregue la palabra a un conjunto (para evitar duplicados) y a una lista (para el orden); (2) tenga método contar_palabras() que retorne cuántas palabras únicas hay; (3) tenga método agregar_multiples(*args) que reutilice agregar_palabra para varios.
class AnalizadorTexto:
    def __init__(self):
        self.unicas = set()      # conjunto para evitar duplicados
        self.orden = []          # lista para mantener el orden de llegada

    def agregar_palabra(self, palabra):
        if palabra not in self.unicas:
            self.unicas.add(palabra)
            self.orden.append(palabra)

    def contar_palabras(self):
        return len(self.unicas)

    def agregar_multiples(self, *args):
        for palabra in args:
            self.agregar_palabra(palabra)


a = AnalizadorTexto()
a.agregar_multiples("hola", "mundo", "hola", "python", "mundo")
print(a.orden)             # ['hola', 'mundo', 'python']
print(a.contar_palabras()) # 3

# 3 Gestor de compras con totales
# Clase CarroCompras que: (1) tenga método agregar_articulo(nombre, precio) que guarde en un diccionario {nombre: precio}; (2) tenga método total_carrito() que retorne la suma de todos los precios; (3) tenga método articulos_por_rango(precio_min, precio_max) que retorne una lista con artículos dentro del rango.
class CarroCompras:
    def __init__(self):
        self.articulos = {}  # diccionario {nombre: precio}

    def agregar_articulo(self, nombre, precio):
        self.articulos[nombre] = precio

    def total_carrito(self):
        return sum(self.articulos.values())

    def articulos_por_rango(self, precio_min, precio_max):
        resultado = []
        for nombre, precio in self.articulos.items():
            if precio_min <= precio <= precio_max:
                resultado.append(nombre)
        return resultado


carro = CarroCompras()
carro.agregar_articulo("Manzana", 1.5)
carro.agregar_articulo("Leche", 3.2)
carro.agregar_articulo("Pan", 2.0)
carro.agregar_articulo("Chocolate", 4.8)

print(carro.total_carrito())                    
print(carro.articulos_por_rango(1.5, 3.5))

# 4 Inversor de secuencias
# Clase InversorSecuencia que: (1) tenga método invertir_lista(lista) que retorne la lista invertida sin usar reversed() (usa manual con bucles); (2) tenga método invertir_multiples(*listas) que reutilice el anterior para invertir varias listas y retorne un diccionario {lista_original: lista_invertida}.
class InversorSecuencia:
    def invertir_lista(self, lista):
        invertida = []
        for i in range(len(lista) - 1, -1, -1):
            invertida.append(lista[i])
        return invertida

    def invertir_multiples(self, *listas):
        resultado = {}
        for lista in listas:
            clave = tuple(lista)  # convertimos a tupla para usar como clave
            resultado[clave] = self.invertir_lista(lista)
        return resultado


inv = InversorSecuencia()
print(inv.invertir_lista([1, 2, 3, 4]))# [4, 3, 2, 1]
print(inv.invertir_multiples([1, 2, 3], ["a", "b", "c"], [10, 20]))
# {(1, 2, 3): [3, 2, 1], ('a', 'b', 'c'): ['c', 'b', 'a'], (10, 20): [20, 10]}

# 5 Detector de números pares e impares
# Clase AnalizadorNumeros que: (1) tenga método es_par(numero) que retorne True/False; (2) tenga método separar(*numeros) que retorne un diccionario {'pares': [...], 'impares': [...]} reutilizando es_par; (3) tenga método cantidad_pares_impares() que retorne una tupla (cant_pares, cant_impares).
class AnalizadorNumeros:
    def __init__(self):
        self.pares = []
        self.impares = []

    def es_par(self, numero):
        return numero % 2 == 0

    def separar(self, *numeros):
        for numero in numeros:
            if self.es_par(numero):
                self.pares.append(numero)
            else:
                self.impares.append(numero)
        return {"pares": self.pares, "impares": self.impares}

    def cantidad_pares_impares(self):
        return (len(self.pares), len(self.impares))

a = AnalizadorNumeros()
print(a.separar(4, 7, 10, 3, 8, 15))# {'pares': [4, 10, 8], 'impares': [7, 3, 15]}
print(a.cantidad_pares_impares())# (3, 3)

# 6 Estadísticas de temperatura
# Clase GestorTemperatura que: (1) tenga método registrar_temperatura(temp) que guarde en una lista; (2) tenga método minima()`, `maxima()`, `promedio() que calculen estadísticas; (3) tenga método registrar_multiples(*temps) que reutilice el registro para varias temperaturas.
class GestorTemperatura:
    def __init__(self):
        self.temperaturas = []

    def registrar_temperatura(self, temp):
        self.temperaturas.append(temp)

    def minima(self):
        if not self.temperaturas:
            return None
        return min(self.temperaturas)

    def maxima(self):
        if not self.temperaturas:
            return None
        return max(self.temperaturas)

    def promedio(self):
        if not self.temperaturas:
            return None
        return sum(self.temperaturas) / len(self.temperaturas)

    def registrar_multiples(self, *temps):
        for temp in temps:
            self.registrar_temperatura(temp)


g = GestorTemperatura()
g.registrar_multiples(22.5, 18.0, 25.3, 19.8, 30.1)

print(g.minima())    
print(g.maxima())    
print(g.promedio())

# 7 Mapeador de edades
# Clase GestorPersonas que: (1) tenga método agregar_persona(nombre, edad) que guarde en un diccionario; (2) tenga método personas_mayores(edad_minima) que retorne una lista de nombres cuya edad sea ≥; (3) tenga método edad_promedio() que retorne el promedio de edades.
class GestorPersonas:
    def __init__(self):
        self.personas = {}  # diccionario {nombre: edad}

    def agregar_persona(self, nombre, edad):
        self.personas[nombre] = edad

    def personas_mayores(self, edad_minima):
        resultado = []
        for nombre, edad in self.personas.items():
            if edad >= edad_minima:
                resultado.append(nombre)
        return resultado

    def edad_promedio(self):
        if not self.personas:
            return 0
        return sum(self.personas.values()) / len(self.personas)


g = GestorPersonas()
g.agregar_persona("Ana", 25)
g.agregar_persona("Luis", 17)
g.agregar_persona("Carla", 32)
g.agregar_persona("Pedro", 19)

print(g.personas_mayores(20))
print(g.edad_promedio())

# 8 Asignador de equipos
# Clase Equipos que: (1) tenga método crear_equipo(nombre_equipo) que inicie un equipo como una lista vacía en un diccionario; (2) tenga método agregar_jugador(equipo, jugador) que añada el jugador al equipo; (3) tenga método equipo_mayor_integrantes() que retorne el nombre del equipo con más jugadores.
class Equipos:
    def __init__(self):
        self.equipos = {}  # diccionario {nombre_equipo: [jugadores]}

    def crear_equipo(self, nombre_equipo):
        self.equipos[nombre_equipo] = []

    def agregar_jugador(self, equipo, jugador):
        self.equipos[equipo].append(jugador)

    def equipo_mayor_integrantes(self):
        if not self.equipos:
            return None
        mayor = None
        cantidad_max = -1
        for nombre, jugadores in self.equipos.items():
            if len(jugadores) > cantidad_max:
                cantidad_max = len(jugadores)
                mayor = nombre
        return mayor


e = Equipos()
e.crear_equipo("Tigres")
e.crear_equipo("Leones")

e.agregar_jugador("Tigres", "Juan")
e.agregar_jugador("Tigres", "Pedro")
e.agregar_jugador("Tigres", "Ana")
e.agregar_jugador("Leones", "Carla")

print(e.equipo_mayor_integrantes())

# 9 Validador de caracteres
# Clase AnalizadorString que: (1) tenga método solo_vocales(letra) que retorne True si es vocal; (2) tenga método contar_por_tipo(texto) que retorne un diccionario {'vocales': cant, 'consonantes': cant, 'digitos': cant} reutilizando métodos; (3) tenga atributo que guarde el texto más largo analizado.
class AnalizadorString:
    def __init__(self):
        self.texto_mas_largo = ""  # atributo que guarda el texto más largo analizado

    def solo_vocales(self, letra):
        return letra.lower() in "aeiou"

    def contar_por_tipo(self, texto):
        vocales = 0
        consonantes = 0
        digitos = 0

        for caracter in texto:
            if caracter.isalpha():
                if self.solo_vocales(caracter):
                    vocales += 1
                else:
                    consonantes += 1
            elif caracter.isdigit():
                digitos += 1

        # Actualiza el texto más largo analizado hasta ahora
        if len(texto) > len(self.texto_mas_largo):
            self.texto_mas_largo = texto

        return {"vocales": vocales, "consonantes": consonantes, "digitos": digitos}


a = AnalizadorString()
print(a.contar_por_tipo("Hola Mundo 2024"))
print(a.contar_por_tipo("Python3"))
print(a.texto_mas_largo)

# Gestor de tareas con prioridad
# Clase Tareas que: (1) tenga método agregar_tarea(descripcion, prioridad) que guarde en una lista de tuplas (descripción, prioridad); (2) tenga método tareas_prioritarias() que retorne solo las de prioridad alta; (3) tenga método eliminar_completada(descripcion) que borre la tarea de la lista.
class Tareas:
    def __init__(self):
        self.tareas = []  # lista de tuplas (descripcion, prioridad)

    def agregar_tarea(self, descripcion, prioridad):
        self.tareas.append((descripcion, prioridad))

    def tareas_prioritarias(self):
        resultado = []
        for descripcion, prioridad in self.tareas:
            if prioridad.lower() == "alta":
                resultado.append(descripcion)
        return resultado

    def eliminar_completada(self, descripcion):
        for tarea in self.tareas:
            if tarea[0] == descripcion:
                self.tareas.remove(tarea)
                break


t = Tareas()
t.agregar_tarea("Estudiar Python", "alta")
t.agregar_tarea("Lavar el auto", "baja")
t.agregar_tarea("Entregar informe", "alta")
t.agregar_tarea("Comprar pan", "media")

print(t.tareas_prioritarias())
t.eliminar_completada("Lavar el auto")
print(t.tareas)

# 11 Contador de frecuencia
# Clase ContadorFrecuencia que: (1) tenga método agregar_elemento(elemento) que guarde en un diccionario contando repeticiones; (2) tenga método elemento_mas_frecuente() que retorne el elemento con mayor frecuencia; (3) tenga método frecuencia_elemento(elemento) que retorne cuántas veces aparece.
class ContadorFrecuencia:
    def __init__(self):
        self.frecuencias = {}  # diccionario {elemento: cantidad}

    def agregar_elemento(self, elemento):
        if elemento in self.frecuencias:
            self.frecuencias[elemento] += 1
        else:
            self.frecuencias[elemento] = 1

    def elemento_mas_frecuente(self):
        if not self.frecuencias:
            return None
        mayor = None
        cantidad_max = -1
        for elemento, cantidad in self.frecuencias.items():
            if cantidad > cantidad_max:
                cantidad_max = cantidad
                mayor = elemento
        return mayor

    def frecuencia_elemento(self, elemento):
        return self.frecuencias.get(elemento, 0)


c = ContadorFrecuencia()
for palabra in ["gato", "perro", "gato", "loro", "gato", "perro"]:
    c.agregar_elemento(palabra)

print(c.frecuencias)
print(c.elemento_mas_frecuente())
print(c.frecuencia_elemento("perro"))
print(c.frecuencia_elemento("pez"))


# 12cSelector de rango con tuplas
# Clase SelectorRango que: (1) tenga método crear_rango(inicio, fin) que retorne una tupla con números en ese rango; (2) tenga método elementos_en_multiples_rangos(*rangos) que reciba múltiples tuplas (inicio,fin) y retorne una lista combinada sin duplicados usando un conjunto.
class SelectorRango:
    def crear_rango(self, inicio, fin):
        return tuple(range(inicio, fin + 1))

    def elementos_en_multiples_rangos(self, *rangos):
        conjunto = set()
        for inicio, fin in rangos:
            numeros = self.crear_rango(inicio, fin)
            conjunto.update(numeros)
        return list(conjunto)


s = SelectorRango()

print(s.crear_rango(1, 5))
# (1, 2, 3, 4, 5)

print(s.elementos_en_multiples_rangos((1, 5), (3, 8), (10, 12)))
# [1, 2, 3, 4, 5, 6, 7, 8, 10, 11, 12]  (orden puede variar, es un set)


# 13 Combinador de listas
# Clase CombinadorListas que: (1) tenga método intercalar(lista1, lista2) que retorne una lista alternando elementos de ambas; (2) tenga método intercalar_multiples(*listas) que reutilice para varias listas.
# Entrada
class CombinadorListas:
    def intercalar(self, lista1, lista2):
        resultado = []
        largo_max = max(len(lista1), len(lista2))
        for i in range(largo_max):
            if i < len(lista1):
                resultado.append(lista1[i])
            if i < len(lista2):
                resultado.append(lista2[i])
        return resultado

    def intercalar_multiples(self, *listas):
        resultado = []
        largo_max = max(len(lista) for lista in listas)
        for i in range(largo_max):
            for lista in listas:
                if i < len(lista):
                    resultado.append(lista[i])
        return resultado


c = CombinadorListas()

print(c.intercalar([1, 2, 3], ["a", "b", "c"]))
# [1, 'a', 2, 'b', 3, 'c']

print(c.intercalar([1, 2, 3], ["a", "b"]))
# [1, 'a', 2, 'b', 3]

print(c.intercalar_multiples([1, 2, 3], ["a", "b"], ["x", "y", "z", "w"]))
# [1, 'a', 'x', 2, 'b', 'y', 3, 'z', 'w']


# 14 Mapeo de estudiantes a notas
# Clase RegistroNotas que: (1) tenga método registrar(estudiante, nota) que guarde en un diccionario; (2) tenga método estudiantes_aprobados(nota_minima) que retorne lista de estudiantes; (3) tenga método mejor_estudiante() que retorne nombre y nota del que tiene mayor calificación.
class RegistroNotas:
    def __init__(self):
        self.notas = {}  # diccionario {estudiante: nota}

    def registrar(self, estudiante, nota):
        self.notas[estudiante] = nota

    def estudiantes_aprobados(self, nota_minima):
        resultado = []
        for estudiante, nota in self.notas.items():
            if nota >= nota_minima:
                resultado.append(estudiante)
        return resultado

    def mejor_estudiante(self):
        if not self.notas:
            return None
        mejor_nombre = None
        mejor_nota = -1
        for estudiante, nota in self.notas.items():
            if nota > mejor_nota:
                mejor_nota = nota
                mejor_nombre = estudiante
        return (mejor_nombre, mejor_nota)


r = RegistroNotas()
r.registrar("Ana", 85)
r.registrar("Luis", 62)
r.registrar("Carla", 93)
r.registrar("Pedro", 78)

print(r.estudiantes_aprobados(70))
print(r.mejor_estudiante())


# 15 Divisores de un número
# Clase DivisorFinder que: (1) tenga método encontrar_divisores(numero) que retorne una tupla con todos los divisores; (2) tenga método es_perfecto(numero) que retorne True si la suma de sus divisores (excepto él mismo) es igual a él; (3) tenga método encontrar_multiples_divisores(*numeros) que retorne un diccionario {número: tupla_divisores}.
class DivisorFinder:
    def encontrar_divisores(self, numero):
        divisores = []
        for i in range(1, numero + 1):
            if numero % i == 0:
                divisores.append(i)
        return tuple(divisores)

    def es_perfecto(self, numero):
        divisores = self.encontrar_divisores(numero)
        suma = sum(divisores) - numero  # se excluye el número mismo
        return suma == numero

    def encontrar_multiples_divisores(self, *numeros):
        resultado = {}
        for numero in numeros:
            resultado[numero] = self.encontrar_divisores(numero)
        return resultado


d = DivisorFinder()

print(d.encontrar_divisores(28))
# (1, 2, 4, 7, 14, 28)

print(d.es_perfecto(28))
# True  → 1+2+4+7+14 = 28

print(d.es_perfecto(10))
# False → 1+2+5 = 8, no es igual a 10

print(d.encontrar_multiples_divisores(6, 28, 12))
# {6: (1, 2, 3, 6), 28: (1, 2, 4, 7, 14, 28), 12: (1, 2, 3, 4, 6, 12)}


# 16 Codificador/Decodificador
# Clase CodificadorCesar que: (1) tenga método codificar_letra(letra, desplazamiento) que retorne la letra desplazada en el alfabeto (usar operador %); (2) tenga método codificar_palabra(palabra, desplazamiento) que reutilice para toda la palabra; (3) tenga un diccionario como atributo para historial de codificaciones.
class CodificadorCesar:
    def __init__(self):
        self.historial = {}  # {palabra_original: palabra_codificada}

    def codificar_letra(self, letra, desplazamiento):
        if letra.isalpha():
            base = ord('A') if letra.isupper() else ord('a')
            posicion = ord(letra) - base
            nueva_posicion = (posicion + desplazamiento) % 26
            return chr(base + nueva_posicion)
        else:
            return letra  # deja igual espacios, números, símbolos

    def codificar_palabra(self, palabra, desplazamiento):
        resultado = ""
        for letra in palabra:
            resultado += self.codificar_letra(letra, desplazamiento)
        self.historial[palabra] = resultado
        return resultado


c = CodificadorCesar()
print(c.codificar_palabra("Hola Mundo", 3))
# Krod Pxqgr
print(c.codificar_palabra("Python", 5))
# Udymts
print(c.historial)
# {'Hola Mundo': 'Krod Pxqgr', 'Python': 'Udymts'}


# 17 Grupo de edades
# Clase AgrupadorEdades que: (1) tenga método clasificar_edad(edad) que retorne la categoría ("niño", "adolescente", "adulto", "mayor"); (2) tenga método agrupar_por_categoria(*edades) que retorne un diccionario con {categoría: [edades]}; (3) tenga método edad_promedio_categoria(categoria).
class AgrupadorEdades:
    def __init__(self):
        self.grupos = {}  # se llena al usar agrupar_por_categoria

    def clasificar_edad(self, edad):
        if edad <= 12:
            return "niño"
        elif edad <= 17:
            return "adolescente"
        elif edad <= 64:
            return "adulto"
        else:
            return "mayor"

    def agrupar_por_categoria(self, *edades):
        for edad in edades:
            categoria = self.clasificar_edad(edad)
            if categoria not in self.grupos:
                self.grupos[categoria] = []
            self.grupos[categoria].append(edad)
        return self.grupos

    def edad_promedio_categoria(self, categoria):
        if categoria not in self.grupos or not self.grupos[categoria]:
            return None
        edades = self.grupos[categoria]
        return sum(edades) / len(edades)


a = AgrupadorEdades()
print(a.agrupar_por_categoria(5, 15, 25, 70, 8, 45, 80, 16))
print(a.edad_promedio_categoria("adulto"))
print(a.edad_promedio_categoria("mayor"))


# 18 Matriz de distancias
# Clase CalculadorDistancia que: (1) tenga método distancia_euclidiana(p1, p2) que reciba dos tuplas (x,y) y calcule la distancia; (2) tenga método punto_mas_cercano(referencia, *puntos) que retorne el punto más cercano a referencia; (3) tenga un atributo lista para guardar todas las distancias calculadas.
import math

class CalculadorDistancia:
    def __init__(self):
        self.distancias_calculadas = []  # guarda cada distancia calculada

    def distancia_euclidiana(self, p1, p2):
        x1, y1 = p1
        x2, y2 = p2
        distancia = math.sqrt((x2 - x1) ** 2 + (y2 - y1) ** 2)
        self.distancias_calculadas.append(distancia)
        return distancia

    def punto_mas_cercano(self, referencia, *puntos):
        mas_cercano = None
        menor_distancia = None
        for punto in puntos:
            d = self.distancia_euclidiana(referencia, punto)
            if menor_distancia is None or d < menor_distancia:
                menor_distancia = d
                mas_cercano = punto
        return mas_cercano


c = CalculadorDistancia()
print(c.distancia_euclidiana((0, 0), (3, 4)))
# 5.0
print(c.punto_mas_cercano((0, 0), (5, 5), (1, 1), (10, 10), (2, 2)))
# (1, 1)
print(c.distancias_calculadas)
# [5.0, 7.0710678118654755, 1.4142135623730951, 14.142135623730951, 2.8284271247461903]


# 19 Inventario de productos
# Clase Inventario que: (1) tenga método agregar_stock(producto, cantidad) que guarde en un diccionario; (2) tenga método restar_stock(producto, cantidad) que disminuya y retorne True si hay suficiente; (3) tenga método productos_bajo_stock(minimo) que retorne una lista de productos con cantidad < minimo.
class Inventario:
    def __init__(self):
        self.stock = {}  # diccionario {producto: cantidad}

    def agregar_stock(self, producto, cantidad):
        if producto in self.stock:
            self.stock[producto] += cantidad
        else:
            self.stock[producto] = cantidad

    def restar_stock(self, producto, cantidad):
        if producto not in self.stock or self.stock[producto] < cantidad:
            return False
        self.stock[producto] -= cantidad
        return True

    def productos_bajo_stock(self, minimo):
        resultado = []
        for producto, cantidad in self.stock.items():
            if cantidad < minimo:
                resultado.append(producto)
        return resultado


inv = Inventario()
inv.agregar_stock("Manzanas", 50)
inv.agregar_stock("Peras", 8)
inv.agregar_stock("Naranjas", 20)
inv.agregar_stock("Manzanas", 10)  # se suma al stock existente

print(inv.stock)
print(inv.restar_stock("Manzanas", 30))
print(inv.restar_stock("Peras", 100))
print(inv.stock)
print(inv.productos_bajo_stock(15))


# 20 Analizador de patrones en textos
# Clase AnalizadorPatrones que: (1) tenga método encontrar_palabras(texto, patron) que busque palabras que inicien con el patrón y retorne una lista; (2) tenga método agrupar_por_longitud(texto) que retorne un diccionario {longitud: [palabras]}; (3) tenga método palabras_unicas() usando un conjunto.
class AnalizadorPatrones:
    def __init__(self):
        self.todas_palabras = []  # guarda todas las palabras vistas hasta ahora

    def encontrar_palabras(self, texto, patron):
        palabras = texto.split()
        self.todas_palabras.extend(palabras)
        resultado = []
        for palabra in palabras:
            if palabra.lower().startswith(patron.lower()):
                resultado.append(palabra)
        return resultado

    def agrupar_por_longitud(self, texto):
        palabras = texto.split()
        self.todas_palabras.extend(palabras)
        grupos = {}
        for palabra in palabras:
            longitud = len(palabra)
            if longitud not in grupos:
                grupos[longitud] = []
            grupos[longitud].append(palabra)
        return grupos

    def palabras_unicas(self):
        return list(set(self.todas_palabras))


a = AnalizadorPatrones()

print(a.encontrar_palabras("El perro corre por el parque", "p"))
# ['perro', 'por', 'parque']

print(a.agrupar_por_longitud("Hola mundo feliz hoy"))
# {4: ['Hola', 'hoy'], 5: ['mundo', 'feliz']}

print(a.palabras_unicas())
# lista con todas las palabras únicas vistas hasta ahora (de ambas llamadas)

#20 ejercicios similares
# 1. Validador de precios
#Clase Verificador que: (1) tenga método validar_precio(precio) que retorne True si 0 ≤ precio ≤ 10000; (2) tenga método cargar_precios(*args) que valide y guarde solo los válidos en una lista; (3) tenga método precio_total() que retorne la suma de los precios almacenados.
class Verificador:
    def __init__(self):
        self.precios = []

    def validar_precio(self, precio):
        return 0 <= precio <= 10000

    def cargar_precios(self, *args):
        for precio in args:
            if self.validar_precio(precio):
                self.precios.append(precio)
        return self.precios

    def precio_total(self):
        return sum(self.precios)

v = Verificador()
print(v.cargar_precios(500, 15000, 200, -50, 999))
print(v.precio_total())

# 2. Contador de ingredientes únicos
# Clase AnalizadorReceta que: (1) tenga método agregar_ingrediente(ingrediente) que lo guarde en un conjunto y en una lista ordenada; (2) tenga método contar_ingredientes() que retorne cuántos ingredientes únicos hay; (3) tenga método agregar_multiples(*args) que reutilice agregar_ingrediente.
class AnalizadorReceta:
    def __init__(self):
        self.unicos = set()
        self.orden = []

    def agregar_ingrediente(self, ingrediente):
        if ingrediente not in self.unicos:
            self.unicos.add(ingrediente)
            self.orden.append(ingrediente)

    def contar_ingredientes(self):
        return len(self.unicos)

    def agregar_multiples(self, *args):
        for ingrediente in args:
            self.agregar_ingrediente(ingrediente)

r = AnalizadorReceta()
r.agregar_multiples("sal", "azucar", "sal", "harina")
print(r.orden)
print(r.contar_ingredientes())


# 3. Gestor de biblioteca con costos
# Clase Biblioteca que: (1) tenga método agregar_libro(titulo, costo_multa) que guarde en un diccionario; (2) tenga método total_multas() que retorne la suma de todas las multas; (3) tenga método libros_por_rango(costo_min, costo_max) que retorne los libros dentro de ese rango.
class Biblioteca:
    def __init__(self):
        self.libros = {}

    def agregar_libro(self, titulo, costo_multa):
        self.libros[titulo] = costo_multa

    def total_multas(self):
        return sum(self.libros.values())

    def libros_por_rango(self, costo_min, costo_max):
        resultado = []
        for titulo, costo in self.libros.items():
            if costo_min <= costo <= costo_max:
                resultado.append(titulo)
        return resultado

b = Biblioteca()
b.agregar_libro("Cien años de soledad", 5.0)
b.agregar_libro("1984", 2.5)
b.agregar_libro("El Principito", 1.0)
print(b.total_multas())
print(b.libros_por_rango(1.0, 3.0))


# 4. Rotador de listas
# Clase RotadorSecuencia que: (1) tenga método rotar_lista(lista, pasos) que mueva los primeros pasos elementos al final (sin usar slicing con [:] directo, hazlo con bucle); (2) tenga método rotar_multiples(*listas, pasos) que reutilice el anterior para varias listas y retorne un diccionario {lista_original: lista_rotada}.
class RotadorSecuencia:
    def rotar_lista(self, lista, pasos):
        rotada = []
        largo = len(lista)
        for i in range(largo):
            nueva_posicion = (i - pasos) % largo
            rotada.append(lista[nueva_posicion])
        return rotada

    def rotar_multiples(self, *listas, pasos):
        resultado = {}
        for lista in listas:
            clave = tuple(lista)
            resultado[clave] = self.rotar_lista(lista, pasos)
        return resultado

rot = RotadorSecuencia()
print(rot.rotar_lista([1, 2, 3, 4], 2))
print(rot.rotar_multiples([1, 2, 3], ["a", "b", "c"], pasos=1))


# 5. Detector de números primos
# Clase AnalizadorPrimos que: (1) tenga método es_primo(numero) que retorne True/False; (2) tenga método separar(*numeros) que retorne un diccionario {'primos': [...], 'no_primos': [...]} reutilizando es_primo; (3) tenga método cantidad_primos_no_primos() que retorne una tupla (cant_primos, cant_no_primos).
class AnalizadorPrimos:
    def __init__(self):
        self.primos = []
        self.no_primos = []

    def es_primo(self, numero):
        if numero < 2:
            return False
        for i in range(2, numero):
            if numero % i == 0:
                return False
        return True

    def separar(self, *numeros):
        for numero in numeros:
            if self.es_primo(numero):
                self.primos.append(numero)
            else:
                self.no_primos.append(numero)
        return {"primos": self.primos, "no_primos": self.no_primos}

    def cantidad_primos_no_primos(self):
        return (len(self.primos), len(self.no_primos))

ap = AnalizadorPrimos()
print(ap.separar(2, 4, 7, 9, 11, 15))
print(ap.cantidad_primos_no_primos())

# 6. Estadísticas de ventas diarias
# Clase GestorVentas que: (1) tenga método registrar_venta(monto) que guarde en una lista; (2) tenga método venta_minima(), venta_maxima(), venta_promedio() que calculen estadísticas; (3) tenga método registrar_multiples(*montos) que reutilice el registro.
class GestorVentas:
    def __init__(self):
        self.ventas = []

    def registrar_venta(self, monto):
        self.ventas.append(monto)

    def venta_minima(self):
        return min(self.ventas) if self.ventas else None

    def venta_maxima(self):
        return max(self.ventas) if self.ventas else None

    def venta_promedio(self):
        return sum(self.ventas) / len(self.ventas) if self.ventas else None

    def registrar_multiples(self, *montos):
        for monto in montos:
            self.registrar_venta(monto)

gv = GestorVentas()
gv.registrar_multiples(150.5, 200.0, 89.9, 320.75)
print(gv.venta_minima())
print(gv.venta_maxima())
print(gv.venta_promedio())


# 7. Mapeo de empleados a salarios
# Clase GestorEmpleados que: (1) tenga método agregar_empleado(nombre, salario) que guarde en un diccionario; (2) tenga método empleados_bien_pagados(salario_minimo) que retorne una lista de nombres cuyo salario sea ≥; (3) tenga método salario_promedio() que retorne el promedio de salarios.
class GestorEmpleados:
    def __init__(self):
        self.empleados = {}

    def agregar_empleado(self, nombre, salario):
        self.empleados[nombre] = salario

    def empleados_bien_pagados(self, salario_minimo):
        resultado = []
        for nombre, salario in self.empleados.items():
            if salario >= salario_minimo:
                resultado.append(nombre)
        return resultado

    def salario_promedio(self):
        if not self.empleados:
            return 0
        return sum(self.empleados.values()) / len(self.empleados)

ge = GestorEmpleados()
ge.agregar_empleado("Marta", 1200)
ge.agregar_empleado("Jose", 800)
ge.agregar_empleado("Elena", 1500)
print(ge.empleados_bien_pagados(1000))
print(ge.salario_promedio())


# 8. Asignador de aulas
# Clase Aulas que: (1) tenga método crear_aula(nombre_aula) que inicie el aula como lista vacía en un diccionario; (2) tenga método agregar_estudiante(aula, estudiante) que añada el estudiante al aula; (3) tenga método aula_menor_ocupacion() que retorne el nombre del aula con menos estudiantes.
class Aulas:
    def __init__(self):
        self.aulas = {}

    def crear_aula(self, nombre_aula):
        self.aulas[nombre_aula] = []

    def agregar_estudiante(self, aula, estudiante):
        self.aulas[aula].append(estudiante)

    def aula_menor_ocupacion(self):
        if not self.aulas:
            return None
        menor = None
        cantidad_min = None
        for nombre, estudiantes in self.aulas.items():
            if cantidad_min is None or len(estudiantes) < cantidad_min:
                cantidad_min = len(estudiantes)
                menor = nombre
        return menor

au = Aulas()
au.crear_aula("A1")
au.crear_aula("A2")
au.agregar_estudiante("A1", "Sofia")
au.agregar_estudiante("A2", "Mario")
au.agregar_estudiante("A2", "Luz")
print(au.aula_menor_ocupacion())


# 9. Validador de símbolos
# Clase AnalizadorTexto2 que: (1) tenga método es_simbolo(caracter) que retorne True si no es letra ni número; (2) tenga método contar_por_tipo(texto) que retorne un diccionario {'letras': cant, 'numeros': cant, 'simbolos': cant} reutilizando métodos; (3) tenga atributo que guarde el texto más corto analizado.
class AnalizadorTexto2:
    def __init__(self):
        self.texto_mas_corto = None

    def es_simbolo(self, caracter):
        return not caracter.isalpha() and not caracter.isdigit()

    def contar_por_tipo(self, texto):
        letras = consonantes = numeros = simbolos = 0
        for caracter in texto:
            if caracter.isalpha():
                letras += 1
            elif caracter.isdigit():
                numeros += 1
            elif self.es_simbolo(caracter):
                simbolos += 1

        if self.texto_mas_corto is None or len(texto) < len(self.texto_mas_corto):
            self.texto_mas_corto = texto

        return {"letras": letras, "numeros": numeros, "simbolos": simbolos}

at2 = AnalizadorTexto2()
print(at2.contar_por_tipo("Hola! 2024 #Python"))
print(at2.texto_mas_corto)

# 10. Gestor de reservas con prioridad
# Clase Reservas que: (1) tenga método agregar_reserva(nombre_cliente, urgencia) que guarde en una lista de tuplas (nombre, urgencia); (2) tenga método reservas_urgentes() que retorne solo las de urgencia "alta"; (3) tenga método cancelar_reserva(nombre_cliente) que borre la reserva de la lista.
class Reservas:
    def __init__(self):
        self.reservas = []

    def agregar_reserva(self, nombre_cliente, urgencia):
        self.reservas.append((nombre_cliente, urgencia))

    def reservas_urgentes(self):
        resultado = []
        for nombre, urgencia in self.reservas:
            if urgencia.lower() == "alta":
                resultado.append(nombre)
        return resultado

    def cancelar_reserva(self, nombre_cliente):
        for reserva in self.reservas:
            if reserva[0] == nombre_cliente:
                self.reservas.remove(reserva)
                break

res = Reservas()
res.agregar_reserva("Carlos", "alta")
res.agregar_reserva("Diana", "baja")
res.agregar_reserva("Elena", "alta")
print(res.reservas_urgentes())
res.cancelar_reserva("Diana")
print(res.reservas)


# 11. Contador de visitas a páginas
# Clase ContadorVisitas que: (1) tenga método registrar_visita(pagina) que guarde en un diccionario contando repeticiones; (2) tenga método pagina_mas_visitada() que retorne la página con más visitas; (3) tenga método visitas_de(pagina) que retorne cuántas veces fue visitada.
class ContadorVisitas:
    def __init__(self):
        self.visitas = {}

    def registrar_visita(self, pagina):
        if pagina in self.visitas:
            self.visitas[pagina] += 1
        else:
            self.visitas[pagina] = 1

    def pagina_mas_visitada(self):
        if not self.visitas:
            return None
        mayor = None
        cantidad_max = -1
        for pagina, cantidad in self.visitas.items():
            if cantidad > cantidad_max:
                cantidad_max = cantidad
                mayor = pagina
        return mayor

    def visitas_de(self, pagina):
        return self.visitas.get(pagina, 0)

cv = ContadorVisitas()
for pagina in ["inicio", "contacto", "inicio", "productos", "inicio"]:
    cv.registrar_visita(pagina)
print(cv.pagina_mas_visitada())
print(cv.visitas_de("contacto"))


# 12. Selector de horarios con tuplas
# Clase SelectorHorario que: (1) tenga método crear_horario(hora_inicio, hora_fin) que retorne una tupla con las horas en ese intervalo; (2) tenga método horas_en_multiples_turnos(*turnos) que reciba múltiples tuplas (inicio, fin) y retorne una lista combinada sin duplicados usando un conjunto.
class SelectorHorario:
    def crear_horario(self, hora_inicio, hora_fin):
        return tuple(range(hora_inicio, hora_fin + 1))

    def horas_en_multiples_turnos(self, *turnos):
        conjunto = set()
        for inicio, fin in turnos:
            horas = self.crear_horario(inicio, fin)
            conjunto.update(horas)
        return list(conjunto)

sh = SelectorHorario()
print(sh.crear_horario(8, 12))
print(sh.horas_en_multiples_turnos((8, 12), (10, 14)))


# 13. Combinador de nombres y apellidos
# Clase CombinadorNombres que: (1) tenga método combinar(nombres, apellidos) que retorne una lista alternando nombre y apellido correspondientes; (2) tenga método combinar_multiples(*listas) que reutilice para combinar varias listas relacionadas (ej. nombres, apellidos, apodos).
class CombinadorNombres:
    def combinar(self, nombres, apellidos):
        resultado = []
        largo_max = max(len(nombres), len(apellidos))
        for i in range(largo_max):
            if i < len(nombres):
                resultado.append(nombres[i])
            if i < len(apellidos):
                resultado.append(apellidos[i])
        return resultado

    def combinar_multiples(self, *listas):
        resultado = []
        largo_max = max(len(lista) for lista in listas)
        for i in range(largo_max):
            for lista in listas:
                if i < len(lista):
                    resultado.append(lista[i])
        return resultado

cn = CombinadorNombres()
print(cn.combinar(["Ana", "Luis"], ["Perez", "Gomez"]))
print(cn.combinar_multiples(["Ana", "Luis"], ["Perez", "Gomez"], ["A", "B", "C"]))


# 14. Mapeo de jugadores a puntajes
# Clase RegistroPuntajes que: (1) tenga método registrar(jugador, puntaje) que guarde en un diccionario; (2) tenga método jugadores_clasificados(puntaje_minimo) que retorne lista de jugadores; (3) tenga método mejor_jugador() que retorne nombre y puntaje del que tiene mayor puntaje.
class RegistroPuntajes:
    def __init__(self):
        self.puntajes = {}

    def registrar(self, jugador, puntaje):
        self.puntajes[jugador] = puntaje

    def jugadores_clasificados(self, puntaje_minimo):
        resultado = []
        for jugador, puntaje in self.puntajes.items():
            if puntaje >= puntaje_minimo:
                resultado.append(jugador)
        return resultado

    def mejor_jugador(self):
        if not self.puntajes:
            return None
        mejor_nombre = None
        mejor_puntaje = -1
        for jugador, puntaje in self.puntajes.items():
            if puntaje > mejor_puntaje:
                mejor_puntaje = puntaje
                mejor_nombre = jugador
        return (mejor_nombre, mejor_puntaje)

rp = RegistroPuntajes()
rp.registrar("Jugador1", 1500)
rp.registrar("Jugador2", 2200)
rp.registrar("Jugador3", 900)
print(rp.jugadores_clasificados(1000))
print(rp.mejor_jugador())


# 15. Múltiplos de un número
# Clase MultiploFinder que: (1) tenga método encontrar_multiplos(numero, limite) que retorne una tupla con los múltiplos de numero hasta limite; (2) tenga método es_abundante(numero) que retorne True si la suma de sus divisores (excepto él mismo) es mayor a él; (3) tenga método encontrar_multiples_multiplos(*numeros, limite) que retorne un diccionario {número: tupla_multiplos}.
class MultiploFinder:
    def encontrar_multiplos(self, numero, limite):
        multiplos = []
        for i in range(numero, limite + 1, numero):
            multiplos.append(i)
        return tuple(multiplos)

    def es_abundante(self, numero):
        divisores = [i for i in range(1, numero) if numero % i == 0]
        return sum(divisores) > numero

    def encontrar_multiples_multiplos(self, *numeros, limite):
        resultado = {}
        for numero in numeros:
            resultado[numero] = self.encontrar_multiplos(numero, limite)
        return resultado

mf = MultiploFinder()
print(mf.encontrar_multiplos(3, 15))
print(mf.es_abundante(12))
print(mf.encontrar_multiples_multiplos(2, 3, limite=10))


# 16. Codificador/Decodificador inverso
# Clase CodificadorAtbash que: (1) tenga método codificar_letra(letra) que retorne la letra reflejada en el alfabeto (A↔Z, B↔Y, usando operador % o resta directa); (2) tenga método codificar_palabra(palabra) que reutilice para toda la palabra; (3) tenga un diccionario como atributo para historial de codificaciones.
class CodificadorAtbash:
    def __init__(self):
        self.historial = {}

    def codificar_letra(self, letra):
        if letra.isalpha():
            base = ord('A') if letra.isupper() else ord('a')
            posicion = ord(letra) - base
            nueva_posicion = 25 - posicion
            return chr(base + nueva_posicion)
        return letra

    def codificar_palabra(self, palabra):
        resultado = ""
        for letra in palabra:
            resultado += self.codificar_letra(letra)
        self.historial[palabra] = resultado
        return resultado

ca = CodificadorAtbash()
print(ca.codificar_palabra("Hola"))
print(ca.historial)


# 17. Grupo de temperaturas
# Clase AgrupadorTemperaturas que: (1) tenga método clasificar_temperatura(temp) que retorne la categoría ("frío", "templado", "cálido", "caluroso"); (2) tenga método agrupar_por_categoria(*temperaturas) que retorne un diccionario {categoría: [temperaturas]}; (3) tenga método temperatura_promedio_categoria(categoria).
class AgrupadorTemperaturas:
    def __init__(self):
        self.grupos = {}

    def clasificar_temperatura(self, temp):
        if temp < 10:
            return "frío"
        elif temp < 20:
            return "templado"
        elif temp < 30:
            return "cálido"
        else:
            return "caluroso"

    def agrupar_por_categoria(self, *temperaturas):
        for temp in temperaturas:
            categoria = self.clasificar_temperatura(temp)
            if categoria not in self.grupos:
                self.grupos[categoria] = []
            self.grupos[categoria].append(temp)
        return self.grupos

    def temperatura_promedio_categoria(self, categoria):
        if categoria not in self.grupos or not self.grupos[categoria]:
            return None
        temps = self.grupos[categoria]
        return sum(temps) / len(temps)

agt = AgrupadorTemperaturas()
print(agt.agrupar_por_categoria(5, 15, 25, 35, 8, 22))
print(agt.temperatura_promedio_categoria("cálido"))


# 18. Matriz de distancias de vuelos
# Clase CalculadorDistanciaVuelo que: (1) tenga método distancia_manhattan(p1, p2) que reciba dos tuplas (x,y) y calcule la distancia Manhattan (|x2-x1| + |y2-y1|); (2) tenga método aeropuerto_mas_lejano(referencia, *puntos) que retorne el punto más lejano a referencia; (3) tenga un atributo lista para guardar todas las distancias calculadas.
class CalculadorDistanciaVuelo:
    def __init__(self):
        self.distancias_calculadas = []

    def distancia_manhattan(self, p1, p2):
        x1, y1 = p1
        x2, y2 = p2
        distancia = abs(x2 - x1) + abs(y2 - y1)
        self.distancias_calculadas.append(distancia)
        return distancia

    def aeropuerto_mas_lejano(self, referencia, *puntos):
        mas_lejano = None
        mayor_distancia = -1
        for punto in puntos:
            d = self.distancia_manhattan(referencia, punto)
            if d > mayor_distancia:
                mayor_distancia = d
                mas_lejano = punto
        return mas_lejano

cdv = CalculadorDistanciaVuelo()
print(cdv.aeropuerto_mas_lejano((0, 0), (3, 4), (10, 10), (1, 1)))
print(cdv.distancias_calculadas)


# 19. Inventario de bodega con alertas
# Clase Bodega que: (1) tenga método agregar_producto(producto, cantidad) que guarde en un diccionario; (2) tenga método sumar_producto(producto, cantidad) que aumente el stock y retorne el nuevo total; (3) tenga método productos_sobre_stock(maximo) que retorne lista de productos con cantidad > máximo.
class Bodega:
    def __init__(self):
        self.stock = {}

    def agregar_producto(self, producto, cantidad):
        self.stock[producto] = cantidad

    def sumar_producto(self, producto, cantidad):
        if producto in self.stock:
            self.stock[producto] += cantidad
        else:
            self.stock[producto] = cantidad
        return self.stock[producto]

    def productos_sobre_stock(self, maximo):
        resultado = []
        for producto, cantidad in self.stock.items():
            if cantidad > maximo:
                resultado.append(producto)
        return resultado

bo = Bodega()
bo.agregar_producto("Tornillos", 500)
bo.sumar_producto("Tornillos", 200)
bo.agregar_producto("Tuercas", 50)
print(bo.stock)
print(bo.productos_sobre_stock(300))


# 20. Analizador de patrones en oraciones
# Clase AnalizadorPatrones2 que: (1) tenga método encontrar_palabras_terminadas_en(texto, patron) que busque palabras que terminen con el patrón y retorne una lista; (2) tenga método agrupar_por_primera_letra(texto) que retorne un diccionario {letra: [palabras]}; (3) tenga método palabras_repetidas() usando un conjunto y una lista para detectar cuáles aparecen más de una vez.
class AnalizadorPatrones2:
    def __init__(self):
        self.todas_palabras = []

    def encontrar_palabras_terminadas_en(self, texto, patron):
        palabras = texto.split()
        self.todas_palabras.extend(palabras)
        resultado = []
        for palabra in palabras:
            if palabra.lower().endswith(patron.lower()):
                resultado.append(palabra)
        return resultado

    def agrupar_por_primera_letra(self, texto):
        palabras = texto.split()
        grupos = {}
        for palabra in palabras:
            letra = palabra[0].lower()
            if letra not in grupos:
                grupos[letra] = []
            grupos[letra].append(palabra)
        return grupos

    def palabras_repetidas(self):
        vistas = set()
        repetidas = set()
        for palabra in self.todas_palabras:
            if palabra in vistas:
                repetidas.add(palabra)
            else:
                vistas.add(palabra)
        return list(repetidas)

ap2 = AnalizadorPatrones2()
print(ap2.encontrar_palabras_terminadas_en("El perro y el gato corren", "n"))
print(ap2.agrupar_por_primera_letra("El perro corre en el parque"))
