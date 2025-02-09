# Java-Review-Exercises-1-
assignment 1

1 find the odd integer
public class FindOdd {
    public static int findIt(int[] a) {
        int result = 0;
        for (int num : a) { // Fixed the variable name
            result ^= num;
        }
        return result;
    }

    public static void main(String[] args) {
        int[] array = {1, 2, 2, 3, 3, 3, 4, 3, 3, 3, 2, 2, 1};
        System.out.println(findIt(array)); // Should print 4
    }
}


2 Convert a Number to a String!
class Kata {
  public static String numberToString(int num) {
    return String.valueOf(num); // Convert integer to string and return
  }
}



3 Reversed Strings
public class Kata {
    public static String solution(String str) {

        return new StringBuilder(str).reverse().toString();
    }

    public static void main(String[] args) {

        System.out.println(solution("world")); // Output: dlrow
        System.out.println(solution("word"));  // Output: drow
    }
}

4 fraction class
public class Fraction implements Comparable<Fraction> {
    private final long top;   // Numerator
    private final long bottom; // Denominator

    // Constructor for Fraction
    public Fraction(long numerator, long denominator) {
        if (denominator == 0) {
            throw new IllegalArgumentException("Denominator cannot be zero");
        }
        // If the denominator is negative, move the negative sign to the numerator
        if (denominator < 0) {
            numerator = -numerator;
            denominator = -denominator;
        }
        this.top = numerator;
        this.bottom = denominator;
    }

    // compare Fraction objects
    @Override
    public int hashCode() {
        return 17 * Long.hashCode(top) + Long.hashCode(bottom);
    }

    @Override
    public boolean equals(Object o) {
        return compareTo((Fraction) o) == 0;
    }

    @Override
    public int compareTo(Fraction f2) {
        return Long.compare(top * f2.bottom, f2.top * bottom);
    }

    private long gcd(long a, long b) {
        while (b != 0) {
            long temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }

    // Simplify the fraction using the GCD
    private Fraction simplify() {
        long gcd = gcd(top, bottom);
        return new Fraction(top / gcd, bottom / gcd);
    }

    // Add two fractions and return the result in simplest form
    public Fraction add(Fraction f2) {
        long commonDenominator = bottom * f2.bottom;
        long newNumerator = top * f2.bottom + f2.top * bottom;
        Fraction result = new Fraction(newNumerator, commonDenominator);
        return result.simplify(); // Simplify the result
    }

    // Make this class string representable in numerator/denominator format
    @Override
    public String toString() {
        return top + "/" + bottom;
    }

    // Main method for testing
    public static void main(String[] args) {
        Fraction fraction1 = new Fraction(4, 5);
        System.out.println(fraction1.add(new Fraction(1, 8)));  // Output: 37/40
    }
}


5 hex class extra
public class Hex {
  private int value;

  // Constructor to initialize the Hex object with a decimal value
  public Hex(int value) {
    this.value = value;
  }

  public int valueOf() {
    return this.value;
  }

  public String toJSON() {
    return toString();
  }

  public String toString() {
    return "0x" + Integer.toHexString(this.value).toUpperCase();
  }

  public Hex plus(Hex other) {
    return new Hex(this.value + other.valueOf());
  }

  public Hex minus(Hex other) {
    return new Hex(this.value - other.valueOf());
  }

  public Hex plus(int number) {
    return new Hex(this.value + number);
  }

  public Hex minus(int number) {
    return new Hex(this.value - number);
  }

  public static int parse(String string) {
    // Check if the string starts with "0x" and remove it if present
    if (string.startsWith("0x")) {
      return Integer.parseInt(string.substring(2), 16);
    } else {
      return Integer.parseInt(string, 16);
    }
  }

  // Method to checks if their values are the same
  @Override
  public boolean equals(Object other) {
    if (this == other) {
      return true;
    }
    if (other == null || getClass() != other.getClass()) {
      return false;
    }
    Hex hex = (Hex) other;
    return this.value == hex.value;
  }


    Hex a = new Hex(10);
    Hex b = new Hex(5);
    System.out.println(a.plus(b).toJSON()); // "0xF"
    System.out.println(a.plus(2).toJSON()); // "0xC"

    System.out.println(Hex.parse("0xFF")); // 255
    System.out.println(Hex.parse("FF")); // 255
  }
}
