import pygame
import pygame.locals as locals

# Initialize Pygame
pygame.init()

# Screen dimensions
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Pygame Game with UNO")

# Colors
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)
BLUE = (0, 0, 255)
RED = (255, 0, 0)

# Fonts
font = pygame.font.Font(None, 74)
small_font = pygame.font.Font(None, 50)

# Button
button_rect = pygame.Rect((WIDTH // 2 - 100, HEIGHT // 2 - 50), (200, 100))

# Load images
floppy_image = pygame.image.load('floppy_disk.png')
floppy_image = pygame.transform.scale(floppy_image, (100, 100))  # Resize floppy disk image

def draw_start_screen():
    screen.fill(BLACK)
    pygame.draw.rect(screen, BLACK, button_rect)
    text = font.render('START GAME', True, WHITE)
    screen.blit(text, (WIDTH // 2 - text.get_width() // 2, HEIGHT // 2 - text.get_height() // 2))
    pygame.display.flip()

def fade_transition(out=True, duration=2000):
    clock = pygame.time.Clock()
    start_ticks = pygame.time.get_ticks()
    alpha = 255 if out else 0
    alpha_step = (255 * 1000 / duration) if out else (-255 * 1000 / duration)
    
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                return
        
        now = pygame.time.get_ticks()
        elapsed = now - start_ticks
        if elapsed > duration:
            break
        
        alpha = min(max(0, alpha + alpha_step), 255)
        fade_surface = pygame.Surface((WIDTH, HEIGHT))
        fade_surface.fill(BLACK)
        fade_surface.set_alpha(alpha)
        screen.blit(fade_surface, (0, 0))
        pygame.display.flip()
        clock.tick(60)

def animate_floppy_disk():
    clock = pygame.time.Clock()
    floppy_rect = floppy_image.get_rect(midright=(WIDTH, HEIGHT // 2))
    target_rect = floppy_image.get_rect(midright=(WIDTH // 2, HEIGHT // 2))
    speed = 5
    
    while floppy_rect.right > target_rect.right:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                return
        
        floppy_rect.x -= speed
        screen.fill(BLACK)
        screen.blit(floppy_image, floppy_rect.topleft)
        pygame.display.flip()
        clock.tick(60)

def draw_uno_game(level, enemy_count, exp):
    screen.fill(BLACK)
    level_text = small_font.render(f'Level: {level}', True, WHITE)
    enemy_text = small_font.render(f'Enemies: {enemy_count}', True, WHITE)
    exp_text = small_font.render(f'EXP: {exp}', True, WHITE)
    
    screen.blit(level_text, (20, 20))
    screen.blit(enemy_text, (20, 60))
    screen.blit(exp_text, (20, 100))
    
    pygame.display.flip()

def main():
    global clock
    clock = pygame.time.Clock()
    game_started = False
    level = 1
    enemy_count = 5
    exp = 0
    
    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                return
            
            if event.type == pygame.MOUSEBUTTONDOWN and not game_started:
                if button_rect.collidepoint(event.pos):
                    game_started = True
                    # Animate floppy disk
                    animate_floppy_disk()
                    pygame.time.wait(1000)  # Wait a bit before the fade transition
                    fade_transition(out=True, duration=5000)  # Fade out in 5 seconds
                    pygame.time.wait(1000)  # Wait a bit before starting the game
                    fade_transition(out=False, duration=5000)  # Fade in in 5 seconds
        
        if not game_started:
            draw_start_screen()
        else:
            draw_uno_game(level, enemy_count, exp)
            # Placeholder for game logic
            pygame.time.wait(2000)  # Simulate game play time
            exp += 10  # Increment experience as a placeholder
            level += 1  # Increment level as a placeholder
            enemy_count += 1  # Increase enemy count as a placeholder

        clock.tick(30)

if __name__ == "__main__":
    main()
