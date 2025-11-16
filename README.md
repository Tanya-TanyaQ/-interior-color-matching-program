# -interior-color-matching-program_________
import colorsys 
import random
import matplotlib.pyplot as plt 
def generate_color_palette(base_color): 
    """Generates a color palette based on a given base color using complementary and analogous schemes.""" 
    r, g, b = base_color
    h, l, s = colorsys.rgb_to_hls(r / 255.0, g / 255.0, b / 255.0)
    # Generate complementary color
    complementary_h = (h + 0.5) % 1.0
    complementary_rgb = colorsys.hls_to_rgb(complementary_h, l, s) 
    complementary_color = tuple(int(c * 255) for c in complementary_rgb) 
    # Generate analogous colors 
    analogous1_h = (h + 0.08) % 1.0
    analogous2_h = (h - 0.08) % 1.0
    analogous1_rgb = colorsys.hls_to_rgb(analogous1_h, l, s)
    analogous2_rgb = colorsys.hls_to_rgb(analogous2_h, l, s)
    analogous_colors = [tuple(int(c * 255) for c in analogous1_rgb),
                        tuple(int(c * 255) for c in analogous2_rgb)]
    
    return [base_color, complementary_color] + analogous_colors

def display_palette(colors):
    """Displays the generated color palette."""
    fig, ax = plt.subplots(1, len(colors), figsize=(10, 2))
    if len(colors) == 1:
        ax = [ax]
    for i, color in enumerate(colors):
        ax[i].imshow([[color]], aspect='auto')
        ax[i].axis('off')
    plt.show()

if __name__ == "__main__":
    # Example: Select a random base color
    base_color = (random.randint(0, 255), random.randint(0, 255), random.randint(0, 255))
    palette = generate_color_palette(base_color)
    print("Generated Color Palette (RGB):", palette)
    display_palette(palette)
