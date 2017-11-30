/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package consoleeapp;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;





public class Consoleeapp {

    static final String JDBC_DRIVER = "com.mysql.jdbc.Driver";
    static final String DB_URL = "jdbc:mysql://localhost:3306/catalog";
    
    static final String USER = "root";
    static final String PASS = "user";
    public static void main(String[] args) throws SQLException, ClassNotFoundException {
         Connection conn = null;
        
        Statement stmt = null;
        try {
            
            Class.forName("com.mysql.jdbc.Driver");
            
            System.out.println("Connecting to database");
            conn = DriverManager.getConnection(DB_URL,USER,PASS);
            System.out.println("Creating statement...");
            stmt = conn.createStatement();
            String sql;
            sql = "SELECT idmembers,f_name,last_name FROM members";
            ResultSet rs = stmt.executeQuery(sql);
            
            while (rs.next()) {
                int member_id = rs.getInt("idmembers");
                String firstname = rs.getString ("f_name");
                String lastname = rs.getString("last_name");
                
                System.out.println("idmembers" + member_id);
                System.out.println(", First name: " + firstname);
                System.out.println(", Last Name: " + lastname);    
            }
            rs.close();
            stmt.close();
            conn.close();
            
        }
        catch(SQLException se) {
            
            se.printStackTrace();
            
        }
        catch(Exception e) {
            e.printStackTrace();
        }
        finally {
            
            
            try {
                if (stmt!=null)
                    stmt.close();
                
            }
            catch(SQLException se2){}
            
            try {
                if (conn!=null)
                    conn.close();
                
            }
            catch(SQLException se) {
                se.printStackTrace();
            }
        }
        
        System.out.println("Finished");
    }
}


    

