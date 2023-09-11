def reconocer_lenguaje(AFND, cadena):
    estados_actuales = {AFND['q0']}  # Comenzamos desde el estado inicial
    for simbolo in cadena:
        nuevos_estados = set()
        for estado in estados_actuales:
            if estado in AFND['δ'] and simbolo in AFND['δ'][estado]:
                nuevos_estados.update(AFND['δ'][estado][simbolo])
        estados_actuales = nuevos_estados

    # Verificamos si hay una intersección entre los estados actuales y los estados finales
    for estado in estados_actuales:
        if estado in AFND['F']:
            return True
    return False

# Ejemplo de uso:
AFND = {
    'Q': {'q0', 'q1'},
    'Σ': {'0', '1'},
    'δ': {
        'q0': {'0': {'q0'}, '1': {'q0', 'q1'}},
        'q1': {'1': {'q1'}}
    },
    'q0': 'q0',
    'F': {'q1'}
}

cadena1 = '0110'
cadena2 = '1010'

if reconocer_lenguaje(AFND, cadena1):
    print(f"'{cadena1}' es aceptada por el AFND.")
else:
    print(f"'{cadena1}' no es aceptada por el AFND.")

if reconocer_lenguaje(AFND, cadena2):
    print(f"'{cadena2}' es aceptada por el AFND.")
else:
    print(f"'{cadena2}' no es aceptada por el AFND.")
