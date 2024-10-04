
1(a) Constructor Overloading, Method Overloading, Static Methods

class Example {
    int value;

    // Constructor Overloading
    Example() {
        value = 0;
    }

    Example(int value) {
        this.value = value;
    }

    // Method Overloading
    void display() {
        System.out.println("Value: " + value);
    }

    void display(String message) {
        System.out.println(message + " " + value);
    }

    // Static method
    static void staticMethod() {
        System.out.println("This is a static method");
    }

    public static void main(String[] args) {
        Example e1 = new Example();
        Example e2 = new Example(10);

        e1.display();
        e2.display("The value is:");
        Example.staticMethod();
    }
}


---

1(b) Inheritance and Method Overriding

class Animal {
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

public class TestInheritance {
    public static void main(String[] args) {
        Animal a = new Animal();
        Dog d = new Dog();
        a.sound();
        d.sound();
    }
}


---

2(a) Abstract Classes and Methods

abstract class Shape {
    abstract void draw();
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing Circle");
    }
}

public class TestAbstract {
    public static void main(String[] args) {
        Shape s = new Circle();
        s.draw();
    }
}


---

2(b) Implementing Interfaces

interface Animal {
    void eat();
}

class Cat implements Animal {
    public void eat() {
        System.out.println("Cat eats");
    }
}

public class TestInterface {
    public static void main(String[] args) {
        Animal a = new Cat();
        a.eat();
    }
}


---

3. User-Defined Exception

class MyException extends Exception {
    MyException(String message) {
        super(message);
    }
}

public class TestException {
    public static void main(String[] args) {
        try {
            throw new MyException("This is a user-defined exception");
        } catch (MyException e) {
            System.out.println(e.getMessage());
        }
    }
}


---

4(a) Methods of List Interface

import java.util.*;

public class TestList {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        System.out.println(list.get(0)); // Accessing elements
        list.remove(1); // Removing element
        System.out.println(list);
    }
}


---

4(b) Methods of Set Interface

import java.util.*;

public class TestSet {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Apple"); // Duplicate, won't be added
        System.out.println(set);
    }
}


---

4(c) Methods of Map Interface

import java.util.*;

public class TestMap {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>();
        map.put(1, "Apple");
        map.put(2, "Banana");
        System.out.println(map.get(1)); // Getting value by key
        map.remove(2); // Removing key-value pair
        System.out.println(map);
    }
}


---

5. Swing Components for Student Resume

import javax.swing.*;

public class ResumeForm {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Student Resume");

        JLabel nameLabel = new JLabel("Name:");
        JTextField nameField = new JTextField();
        nameLabel.setBounds(30, 30, 100, 30);
        nameField.setBounds(150, 30, 150, 30);

        JLabel ageLabel = new JLabel("Age:");
        JTextField ageField = new JTextField();
        ageLabel.setBounds(30, 70, 100, 30);
        ageField.setBounds(150, 70, 150, 30);

        JButton submitButton = new JButton("Submit");
        submitButton.setBounds(100, 110, 100, 30);

        frame.add(nameLabel);
        frame.add(nameField);
        frame.add(ageLabel);
        frame.add(ageField);
        frame.add(submitButton);

        frame.setSize(400, 200);
        frame.setLayout(null);
        frame.setVisible(true);
    }
}


---

6(a) Display Table Data using JDBC

import java.sql.*;

public class DisplayTable {
    public static void main(String[] args) {
        try {
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "password");
            Statement stmt = con.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");

            while (rs.next()) {
                System.out.println(rs.getInt(1) + " " + rs.getString(2));
            }

            con.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}


---

6(b) Return Specific Record from a Table using JDBC

import java.sql.*;

public class GetRecord {
    public static void main(String[] args) {
        try {
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "password");
            PreparedStatement ps = con.prepareStatement("SELECT * FROM students WHERE id=?");
            ps.setInt(1, 1); // Assuming ID is 1

            ResultSet rs = ps.executeQuery();
            while (rs.next()) {
                System.out.println(rs.getInt(1) + " " + rs.getString(2));
            }

            con.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}


---

6(c) Insert/Update/Delete Records using JDBC

import java.sql.*;

public class ModifyRecords {
    public static void main(String[] args) {
        try {
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "password");
            
            // Inserting a record
            PreparedStatement insert = con.prepareStatement("INSERT INTO students VALUES (?, ?)");
            insert.setInt(1, 3);
            insert.setString(2, "John");
            insert.executeUpdate();

            // Updating a record
            PreparedStatement update = con.prepareStatement("UPDATE students SET name=? WHERE id=?");
            update.setString(1, "Jane");
            update.setInt(2, 3);
            update.executeUpdate();

            // Deleting a record
            PreparedStatement delete = con.prepareStatement("DELETE FROM students WHERE id=?");
            delete.setInt(1, 3);
            delete.executeUpdate();

            con.close();
        } catch (Exception e) {
            System.out.println(e);
        }
    }
}


7(a) Simple Calculator using Java Swings

import javax.swing.*;
import java.awt.event.*;

public class Calculator {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Calculator");
        JTextField t1 = new JTextField();
        JTextField t2 = new JTextField();
        JTextField result = new JTextField();
        JButton add = new JButton("Add");
        JButton sub = new JButton("Subtract");

        t1.setBounds(50, 50, 100, 30);
        t2.setBounds(50, 100, 100, 30);
        result.setBounds(50, 150, 100, 30);
        add.setBounds(50, 200, 100, 30);
        sub.setBounds(160, 200, 100, 30);

        add.addActionListener(e -> {
            int a = Integer.parseInt(t1.getText());
            int b = Integer.parseInt(t2.getText());
            result.setText(String.valueOf(a + b));
        });

        sub.addActionListener(e -> {
            int a = Integer.parseInt(t1.getText());
            int b = Integer.parseInt(t2.getText());
            result.setText(String.valueOf(a - b));
        });

        frame.add(t1);
        frame.add(t2);
        frame.add(result);
        frame.add(add);
        frame.add(sub);

        frame.setSize(300, 400);
        frame.setLayout(null);
        frame.setVisible(true);
    }
}


---

7(b) GUI to Accept Details of Record and Submit to Database (JDBC)

import javax.swing.*;
import java.awt.event.*;
import java.sql.*;

public class RecordSubmission {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Record Submission");

        JLabel nameLabel = new JLabel("Name:");
        JTextField nameField = new JTextField();
        JLabel ageLabel = new JLabel("Age:");
        JTextField ageField = new JTextField();
        JButton submitButton = new JButton("Submit");

        nameLabel.setBounds(30, 30, 100, 30);
        nameField.setBounds(150, 30, 150, 30);
        ageLabel.setBounds(30, 70, 100, 30);
        ageField.setBounds(150, 70, 150, 30);
        submitButton.setBounds(100, 110, 100, 30);

        submitButton.addActionListener(e -> {
            String name = nameField.getText();
            int age = Integer.parseInt(ageField.getText());

            try {
                Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "password");
                PreparedStatement ps = con.prepareStatement("INSERT INTO students (name, age) VALUES (?, ?)");
                ps.setString(1, name);
                ps.setInt(2, age);
                ps.executeUpdate();
                con.close();
                JOptionPane.showMessageDialog(null, "Record submitted!");
            } catch (Exception ex) {
                ex.printStackTrace();
            }
        });

        frame.add(nameLabel);
        frame.add(nameField);
        frame.add(ageLabel);
        frame.add(ageField);
        frame.add(submitButton);

        frame.setSize(400, 200);
        frame.setLayout(null);
        frame.setVisible(true);
    }
}


---

8(a) Servlet: Storing and Returning Cookies

Servlet1.java (Storing a Cookie)

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class Servlet1 extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String name = request.getParameter("username");
        Cookie userCookie = new Cookie("username", name);
        response.addCookie(userCookie);
        response.getWriter().println("Cookie stored successfully!");
    }
}

Servlet2.java (Returning the Cookie)

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class Servlet2 extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        Cookie[] cookies = request.getCookies();
        for (Cookie cookie : cookies) {
            if (cookie.getName().equals("username")) {
                response.getWriter().println("Hello, " + cookie.getValue());
            }
        }
    }
}


---

8(b) Servlet: Displaying Cookie Names and Values

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class DisplayCookiesServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        Cookie[] cookies = request.getCookies();
        PrintWriter out = response.getWriter();
        for (Cookie cookie : cookies) {
            out.println("Name: " + cookie.getName() + ", Value: " + cookie.getValue());
        }
    }
}


---

8(c) Servlet: Storing and Returning Session Variable

Servlet1.java (Storing Session Variable)

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class StoreSessionServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String name = request.getParameter("username");
        HttpSession session = request.getSession();
        session.setAttribute("username", name);
        response.getWriter().println("Session variable stored successfully!");
    }
}

Servlet2.java (Returning Session Variable)

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;

public class ReturnSessionServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        HttpSession session = request.getSession();
        String name = (String) session.getAttribute("username");
        response.getWriter().println("Hello, " + name);
    }
}


---

9(a) Registration Servlet to Store Data in the Database

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;

public class RegisterServlet extends HttpServlet {
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String name = request.getParameter("name");
        int age = Integer.parseInt(request.getParameter("age"));

        try {
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "password");
            PreparedStatement ps = con.prepareStatement("INSERT INTO students (name, age) VALUES (?, ?)");
            ps.setString(1, name);
            ps.setInt(2, age);
            ps.executeUpdate();
            con.close();
            response.getWriter().println("Record inserted successfully!");
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}


---

9(b) Servlet to Display All Records of a Table

import java.io.*;
import javax.servlet.*;
import javax.servlet.http.*;
import java.sql.*;

public class DisplayRecordsServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        try {
            Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "password");
            Statement stmt = con.createStatement();
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");

            while (rs.next()) {
                response.getWriter().println(rs.getInt(1) + " " + rs.getString(2) + " " + rs.getInt(3));
            }

            con.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}


---

10(a) JSP to Store and Return Cookie

storeCookie.jsp (Storing a Cookie)

<%
    String name = request.getParameter("username");
    Cookie userCookie = new Cookie("username", name);
    response.addCookie(userCookie);
%>
<p>Cookie stored successfully!</p>

returnCookie.jsp (Returning the Cookie)

<%
    Cookie[] cookies = request.getCookies();
    for (Cookie cookie : cookies) {
        if (cookie.getName().equals("username")) {
            out.println("Hello, " + cookie.getValue());
        }
    }
%>


---

11(a) JSP to Validate User from Database

<%@ page import="java.sql.*" %>
<%
    String username = request.getParameter("username");
    String password = request.getParameter("password");

    try {
        Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/test", "root", "password");
        PreparedStatement ps = con.prepareStatement("SELECT * FROM users WHERE username=? AND password=?");
        ps.setString(1, username);
        ps.setString(2, password);
        ResultSet rs = ps.executeQuery();

        if (rs.next()) {
            out.println("Login successful!");
        } else {
            out.println("Invalid username or password");
        }
        con.close();
    } catch (Exception e) {
        e.printStackTrace();
    }
%>


---

12. Java Application to Encode/Decode JSON

import org.json.JSONObject;

public class JSONExample {
    public static void main(String[] args) {
        // Encoding JSON
        JSONObject obj = new JSONObject();
        obj.put("name", "John");
        obj.put("age", 25);
        System.out.println("Encoded JSON: " + obj.toString());

