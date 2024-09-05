import javax.imageio.ImageIO;
import java.awt.*;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class ImageEnhancer {

    public static void main(String[] args) {
        String inputImagePath = "input.jpg"; // Path to your input image
        String outputImagePath = "output.jpg"; // Path to save the enhanced image
        float brightnessFactor = 1.2f; // Increase brightness (1.0 = original brightness)

        try {
            // Load the image
            BufferedImage image = ImageIO.read(new File(inputImagePath));

            // Enhance the image
            BufferedImage enhancedImage = enhanceImage(image, brightnessFactor);

            // Save the enhanced image
            ImageIO.write(enhancedImage, "jpg", new File(outputImagePath));
            System.out.println("Image enhanced successfully and saved to: " + outputImagePath);

        } catch (IOException e) {
            System.err.println("Error: " + e.getMessage());
        }
    }

    private static BufferedImage enhanceImage(BufferedImage originalImage, float brightnessFactor) {
        // Create a new buffered image to hold the enhanced result
        BufferedImage enhancedImage = new BufferedImage(originalImage.getWidth(), originalImage.getHeight(), originalImage.getType());

        // Iterate through each pixel
        for (int y = 0; y < originalImage.getHeight(); y++) {
            for (int x = 0; x < originalImage.getWidth(); x++) {
                Color pixelColor = new Color(originalImage.getRGB(x, y));

                // Enhance the brightness of the color
                int red = (int) Math.min(255, pixelColor.getRed() * brightnessFactor);
                int green = (int) Math.min(255, pixelColor.getGreen() * brightnessFactor);
                int blue = (int) Math.min(255, pixelColor.getBlue() * brightnessFactor);

                // Set the new RGB value to the enhanced image
                enhancedImage.setRGB(x, y, new Color(red, green, blue).getRGB());
            }
        }

        return enhancedImage;
    }
}
