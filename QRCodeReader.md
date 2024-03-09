import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
import javax.imageio.ImageIO;
import com.google.zxing.BinaryBitmap;
import com.google.zxing.LuminanceSource;
import com.google.zxing.MultiFormatReader;
import com.google.zxing.NotFoundException;
import com.google.zxing.Result;
import com.google.zxing.client.j2se.BufferedImageLuminanceSource;
import com.google.zxing.common.HybridBinarizer;

public class QRCodeReader {
    public static void main(String[] args) {
        String filePath = "path/to/qr_code_image.png"; // Replace with the path to your QR code image file
        try {
            // Read QR code image file
            File qrCodeFile = new File(filePath);
            BufferedImage bufferedImage = ImageIO.read(qrCodeFile);
            
            // Convert image to binary bitmap
            LuminanceSource source = new BufferedImageLuminanceSource(bufferedImage);
            BinaryBitmap bitmap = new BinaryBitmap(new HybridBinarizer(source));
            
            // Decode QR code
            Result result = new MultiFormatReader().decode(bitmap);
            
            // Print QR code contents
            System.out.println("QR Code contents: " + result.getText());
        } catch (IOException e) {
            System.err.println("Error reading QR code image: " + e);
        } catch (NotFoundException e) {
            System.err.println("QR code not found: " + e);
        }
    }
}
