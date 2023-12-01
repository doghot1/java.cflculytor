# java.cflculytor
import java.util.Scanner;

public class END2 {
    public enum RomanNumeral {
        I(1), II(2), III(3), IV(4), V(5), VI(6), VII(7), VIII(8), IX(9), X(10);

        private final int value;

        RomanNumeral(int value) {
            this.value = value;
        }

        public int getValue() {
            return value;
        }
    }

    public static void main(String[] args) {

        Scanner input = new Scanner(System.in);
        System.out.println("Жду действия");

        try {
            String data = input.nextLine();
            String[] array = data.split(" ");
            if (array.length != 3) throw new IllegalArgumentException("Ведите три символа через пробел!");

            String a1 = array[0];
            String oper = array[1];
            String a2 = array[2];
            if (!chekeData(a1, a2)) {
                throw new IllegalArgumentException("ЧИСЛО НЕ ЛЕЖИТ В ПРОМЕЖУТКЕ ОТ 1 ДО 10, ЛИБО РАЗНЫЕ СИСТЕМЫ СЧИСЛЕНИЯ");
            }
            int a = actions(a1, oper, a2);
            if(arabConvertot(a1)&& arabConvertot(a2)){
                System.out.println(a);
            }else{
                System.out.println(Roman(a));
            }
        } catch (Exception u) {
            throw new IllegalArgumentException("ОШИБКА: " + u.getMessage());
        }

    }

    public static boolean chekeData(String number1, String number2) {
        if (arabConvertot(number1) != arabConvertot(number2)) {
            return false;
        }
        int a, b;
        a = concvertor(number1);
        b = concvertor(number2);
        if (a < 1 || a > 10 || b < 1 || b > 10) {
            return false;
        }
        return true;
    }

    //арифметические операции
    public static int actions(String number1, String action, String number2) {
        int a, b;
        a = concvertor(number1);
        b = concvertor(number2);
        switch (action) {
            case "+":
                return a + b;
            case "-":
                return a - b;
            case "/":
                return a / b;
            case "*":
                return a * b;
            default:
                throw new IllegalArgumentException("НЕ КОРЕКТНОЕ ВЫРАЖЕНИЯ!" + " Введите " + "[+, " + " -, " + " /, " + " *]");
        }
    }

    // конвертирует римские числа в арабские
    public static int concvertor(String num1) {
        try {
            return Integer.parseInt(num1);
        } catch (NumberFormatException i) {
            return RomanNumeral.valueOf(num1).getValue();
        }
    }

    // конвертор был созддан что бы проверить условия ввода для метода chekeData
    public static boolean arabConvertot(String steam) {
        try {
            Integer.parseInt(steam);
            return true;
        } catch (Exception e) {
            return false;
        }

    }

    //КОНВЕРТОР АРАБСКИХ ЧИСЕЛ В РИМСКИЕ
    public static String Roman(int number) {
        StringBuilder result = new StringBuilder();
        for (RomanNumeral roman : RomanNumeral.values()) {
            while (number >= roman.getValue()) {
                result.append(roman);
                number -= roman.getValue();
            }
        }
        return result.toString();
    }

