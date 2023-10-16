//琪亚娜，出击！

import java.util.Scanner;

public class PasswordManager {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        while (true) {
            System.out.println("请选择操作：");
            System.out.println("1. 加密");
            System.out.println("2. 解密");
            System.out.println("3. 退出");

            int choice = scanner.nextInt();
            scanner.nextLine(); // 读取多余的换行符

            switch (choice) {
                case 1:
                    System.out.println("请输入要加密的字符串:");
                    String input = scanner.nextLine();
                    String encrypted = encrypt(input);
                    System.out.println("加密后的字符串: " + encrypted);
                    break;
                case 2:
                    System.out.println("请输入要解密的字符串:");
                    String encryptedInput = scanner.nextLine();
                    String decrypted = decrypt(encryptedInput);
                    System.out.println("解密后的字符串: " + decrypted);
                    break;
                case 3:
                    System.out.println("已退出密码管理系统.");
                    return;
                default:
                    System.out.println("无效的选择，请重新输入.");
            }
        }
    }

    public static String encrypt(String input) {
        char[] chars = input.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            chars[i] = (char) (chars[i] + i + 1 + 3); // 加上位置和偏移值
        }
        char temp = chars[0];
        chars[0] = chars[chars.length - 1];
        chars[chars.length - 1] = temp;
        StringBuilder reversed = new StringBuilder(new String(chars)).reverse();
        return reversed.toString();
    }

    public static String decrypt(String input) {
        StringBuilder reversed = new StringBuilder(input).reverse();
        char[] chars = reversed.toString().toCharArray();
        char temp = chars[0];
        chars[0] = chars[chars.length - 1];
        chars[chars.length - 1] = temp;
        for (int i = 0; i < chars.length; i++) {
            chars[i] = (char) (chars[i] - i - 1 - 3); // 减去位置和偏移值
        }
        return new String(chars);
    }
}

