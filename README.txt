import java.util.Scanner;
import java.util.Random;

public class PasswordManager {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("欢迎使用密码管理系统！");

        while (true) {
            System.out.println("请选择操作：");
            System.out.println("1. 加密");
            System.out.println("2. 解密");
            System.out.println("3. 判断密码强度");
            System.out.println("4. 生成密码");
            System.out.println("5. 退出");

            int option = scanner.nextInt();

            switch (option) {
                case 1:
                    System.out.println("请输入密码：");
                    String input = scanner.next();
                    String encrypted = encrypt(input);
                    System.out.println("加密后的密码：");
                    System.out.println(encrypted);
                    break;
                case 2:
                    System.out.println("请输入密码：");
                    String input2 = scanner.next();
                    String decrypted = decrypt(input2);
                    System.out.println("解密后的密码：");
                    System.out.println(decrypted);
                    break;
                case 3:
                    System.out.println("请输入密码：");
                    String input3 = scanner.next();
                    int strength = checkStrength(input3);
                    System.out.println("密码强度：");
                    System.out.println(strength);
                    break;
                case 4:
                    System.out.println("请输入密码长度：");
                    int length = scanner.nextInt();
                    String generated = generatePassword(length);
                    System.out.println("生成的密码：");
                    System.out.println(generated);
                    break;
                case 5:
                    System.out.println("退出系统");
                    System.exit(0);
                    break;
                default:
                    System.out.println("无效的菜单选项，请重新选择");
            }
        }
    }

    private static String encrypt(String input) {
        char[] chars = input.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            chars[i] = (char) (chars[i] + 1 + 3);
        }
        char[] temp = new char[chars.length];
        for (int i = 0; i < chars.length; i++) {
            temp[(chars.length - 1) - i] = chars[i];
        }
        return new String(temp);
    }

    private static String decrypt(String input) {
        char[] chars = input.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            chars[i] = (char) (chars[i] - 1 - 3);
        }
        char[] temp = new char[chars.length];
        for (int i = 0; i < chars.length; i++) {
            temp[i] = chars[chars.length - 1 - i];
        }
        return new String(temp);
    }

    private static int checkStrength(String input) {
        int count = 0;
        for (int i = 0; i < input.length(); i++) {
            char ch = input.charAt(i);
            if (Character.isDigit(ch)) {
                count++;
            } else if (Character.isUpperCase(ch)) {
                count++;
            } else if (Character.isLowerCase(ch)) {
                count++;
            }
        }
        if (input.length() < 8) {
            return 1;
        } else if (count <= 1) {
            return 2;
        } else {
            return 3;
        }
    }

    private static String generatePassword(int length) {
        Random random = new Random();