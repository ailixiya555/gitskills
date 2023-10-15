//琪亚娜，出击！

import com.sun.scenario.Settings;
import java.io.*;
import java.util.Scanner;
public class Mei {
    public static void main(String[] args) {
        Cipher cipher = new Cipher("plaint", "ciphertext", "123456");
        Scanner input = new Scanner(System.in);
        while (true) {
            System.out.println("请选择操作：");
            System.out.println("1. 设置密钥");
            System.out.println("2. 设置明文");
            System.out.println("3. 设置密文");
            System.out.println("4. 加密");
            System.out.println("5. 解密");
            System.out.println("0. 退出");
            int choice = input.nextInt();
            switch (choice) {
                case 1:
                    cipher.setKey();
                    break;
                case 2:
                    System.out.print("请输入明文：");
                    String plaintext = input.next();
                    while (plaintext.length() < 6 || plaintext.length() > 12) {
                        System.out.print("明文长度不符合要求，请重新输入：");
                        plaintext = input.nextLine();
                    }
                    cipher.setPlaintext(plaintext);
                    break;
                case 3:
                    System.out.print("请输入密文（6-12位）：");
                    String ciphertext = input.next();
                    while (ciphertext.length() < 6 || ciphertext.length() > 12) {
                        System.out.print("密文长度不符合要求，请重新输入：");
                        ciphertext = input.nextLine();
                    }
                    cipher.setCiphertext(ciphertext);
                    break;
                case 4:
                    cipher.encryption();
                    break;
                case 5:
                    cipher.decryption();
                    break;
                case 0:
                    return;
                default:
                    System.out.println("输入有误，请重新输入！");
            }
        }
    }
}
class Cipher {
    private String plaintext; // 明文
    private String ciphertext; // 密文
    private String key; // 密钥

    public Cipher(String plaintext, String ciphertext, String key) {
        this.plaintext = plaintext;
        this.ciphertext = ciphertext;
        this.key = key;
    }

    public void setKey() {       //设置密钥
        Scanner input = new Scanner(System.in);
        System.out.print("请输入密钥（6-12位）：");
        String key = input.nextLine();
        while (key.length() < 6 || key.length() > 12) {
            System.out.print("密钥长度不符合要求，请重新输入：");
            key = input.nextLine();
        }
        this.key = key;
    }

    public String getKey() {
        return key;
    }

    public void setPlaintext(String plaintext) {
        this.plaintext = plaintext;
    }

    public String getPlaintext() {
        return plaintext;
    }

    public void setCiphertext(String ciphertext) {
        this.ciphertext = ciphertext;
    }

    public String getCiphertext() {
        return ciphertext;
    }

    public void encryption() {
        char[] keyChars = key.toCharArray();
        int len = keyChars.length;
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < plaintext.length(); i++) {
            char c = plaintext.charAt(i);
            if (c >= 32 && c <= 126) {
                int j = i % len;
                int k = keyChars[j];
                int ascii = (int) c + k;
                if (ascii > 126) {
                    ascii = ascii % 126 + 31;
                }
                sb.append((char) ascii);
            } else {
                sb.append(c);
            }
        }
        ciphertext = sb.toString();
        System.out.println("加密后的密文：" + ciphertext);
    }

    public void decryption() {
        char[] keyChars = key.toCharArray();
        int len = keyChars.length;
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < ciphertext.length(); i++) {
            char c = ciphertext.charAt(i);
            if (c >= 32 && c <= 126) {
                int j = i % len;
                int k = keyChars[j];
                int ascii = (int) c - k;
                if (ascii < 32) {
                    ascii = ascii + 126 - 31;
                }
                sb.append((char) ascii);
            } else {
                sb.append(c);
            }
        }
        plaintext = sb.toString();
        System.out.println("解密后的明文：" + plaintext);
    }
}
