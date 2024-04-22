import java.unit.HashMap;
public class Login {
    private HashMap<String, String> userCredentials;

    public Login() {
        // Initialize userCredentials HashMap to store username-password pairs
        userCredentials = new HashMap<>();
    }

    public boolean checkUserName(String username) {
        // Check if username contains an underscore and is no more than 5 characters long
        return username.matches("^[a-zA-Z0-9_]{1,5}$");
    }

    public boolean checkPasswordComplexity(String password) {
        // Check if password meets complexity requirements
        return password.matches("^(?=.*[a-z])(?=.*[A-Z])(?=.*\\d)(?=.*[@#$%^&+=]).{8,}$");
    }

    public String registerUser(String username, String password) {
        // Check username and password, return appropriate message
        if (!checkUserName(username)) {
            return "Username is not correctly formatted, please ensure that your username contains an underscore and is no more than 5 characters in length.";
        } else if (!checkPasswordComplexity(password)) {
            return "Password is not correctly formatted, please ensure that the password contains at least 8 characters, a capital letter, a number and a special character.";
        } else {
            // Register user successfully by storing username-password pair
            userCredentials.put(username, password);
            return "User registered successfully";
        }
    }

    public boolean loginUser(String username, String password) {
        // Check if the entered username exists and if the password matches
        return userCredentials.containsKey(username) && userCredentials.get(username).equals(password);
    }

    public String returnLoginStatus(boolean loginStatus, String firstName, String lastName) {
        // Return appropriate login status message
        if (loginStatus) {
            return "Welcome " + firstName + " " + lastName + ", it is great to see you.";
        } else {
            return "Username or password incorrect, please try again";
        }
    }

    // Unit tests
    public static void main(String[] args) {
        Login login = new Login();

        // Test cases for registerUser method
        assert login.registerUser("kyl_1", "Ch&&sec@ke99!") == "User registered successfully";
        assert login.registerUser("kyle!!!!!!!", "Ch&&sec@ke99!") == "Username is not correctly formatted, please ensure that your username contains an underscore and is no more than 5 characters in length.";
        assert login.registerUser("kyl_1", "password") == "Password is not correctly formatted, please ensure that the password contains at least 8 characters, a capital letter, a number and a special character.";

        // Test cases for loginUser method
        login.registerUser("test_user", "Test@1234");
        assert login.loginUser("test_user", "Test@1234") == true;
        assert login.loginUser("test_user", "wrong_password") == false;
        
        // Test cases for returnLoginStatus method
        assert login.returnLoginStatus(true, "John", "Doe").equals("Welcome John Doe, it is great to see you.");
        assert login.returnLoginStatus(false, "", "").equals("Username or password incorrect, please try again");
    }
}

