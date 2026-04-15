import pygame

pygame.init()

# Pantalla
pantalla = pygame.display.set_mode((800, 600))
pygame.display.set_caption("Mini Plataforma")

# Colores
BLANCO = (255, 255, 255)
AZUL = (0, 0, 255)

# Jugador
x = 50
y = 500
velocidad = 5
salto = False
fuerza_salto = 10

gravedad = 0.5
vel_y = 0

corriendo = True
reloj = pygame.time.Clock()

while corriendo:
    reloj.tick(60)
    pantalla.fill(BLANCO)

    for evento in pygame.event.get():
        if evento.type == pygame.QUIT:
            corriendo = False

    teclas = pygame.key.get_pressed()

    # Movimiento
    if teclas[pygame.K_LEFT]:
        x -= velocidad
    if teclas[pygame.K_RIGHT]:
        x += velocidad

    # Salto
    if teclas[pygame.K_SPACE] and not salto:
        salto = True
        vel_y = -10

    if salto:
        vel_y += gravedad
        y += vel_y

        if y >= 500:
            y = 500
            salto = False

    # Dibujar jugador
    pygame.draw.rect(pantalla, AZUL, (x, y, 50, 50))

    pygame.display.update()

pygame.quit()
