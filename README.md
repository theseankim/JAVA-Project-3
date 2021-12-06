# JAVA-Project-3
A Student and Course Management System

package finalProject;

import java.util.ArrayList;
import java.util.Collections;
import java.util.Random;
import java.util.Scanner;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.io.File;
import java.io.FileWriter;
import java.io.IOException;
	
	public AndrewKim_Section002_Project2() {
		
	public static void main(String[] args) {
		ArrayList<student> studentList = new ArrayList<student>();
		System.out.println("Welcome to the Student and Course Management System!"); 
		System.out.println("This system will allow you to manage students and courses. Let's start with the number of students"); 
		
		Scanner scan = new Scanner(System.in); 
		System.out.print("This system will have: "); 
		int studentNum = scan.nextInt(); 
		
		int choice = 0;
		int b = 0;
		Scanner sc = new Scanner (System.in);
	
		do {
			System.out.println("\nWelcome to the Student and Course Management System!"); 
			System.out.println("Press ‘1’ for Student Management System (SMS)"); 
			System.out.println("Press ‘2’ for Course Management System (CMS)");
			System.out.println("Press ‘0’ to exit");
			System.out.println("Please enter choice: ");
			choice = sc.nextInt();
	
			switch(choice) {
      
			case 1: 
			do {			
				System.out.println("\nWelcome to Student Management System!");
				System.out.println("Press ‘1’ to add a student"); 
				System.out.println("Press ‘2’ to deactivate a student"); 
				System.out.println("Press ‘3’ to display all students"); 
				System.out.println("Press ‘4’ to search for a student by ID"); 
				System.out.println("Press ‘5’ to assign on-campus job");
				System.out.println("Press ‘6’ to display all students with on-campus jobs");
				
				System.out.println("Press ‘0’ to exit the system"); 
				choice = sc.nextInt();
				switch (choice) {
				//adding a student into the database (first name, last name, and level of student)
				case 1: 
	                //obj.add_student();
					Scanner scan1 = new Scanner(System.in);
					System.out.println("\nEnter the First Name: ");
					String first = scan1.next();
		            System.out.println("Enter the Last Name: ");
		            String last = scan1.next();
		            System.out.println("Enter the level of the Student: ");
		            String level = scan1.next();
		            Random rand = new Random();
		            int id = rand.nextInt(100);
		            studentList.add(new student(id, first, last, level, true, null, null));
		            System.out.println(first + " " + last + " has been added as a " + level + " with ID " + id); 
	                break;
	           //activating/deactivating student based off their ID 
				case 2:
	            	Scanner scan2 = new Scanner(System.in);
	            	System.out.print("Enter the ID for the student you want to activate/deactivate: ");
	            	int findID = scan2.nextInt();
	            	for(student stud : studentList) {
	            		if(stud.getId() == findID) {
	            			if(stud.getActivity() == true) {
		            			stud.setActivity(false);
		            			System.out.print(stud.getFirst_name() + " " + stud.getLast_name() + " has been deactivated\n");
		            			break;
	            			}
	            			else {
	            				stud.setActivity(true);
		            			System.out.print(stud.getFirst_name() + " " + stud.getLast_name() + " has been activated\n");
		            			break;
	            			}
	            		}
	
	            	}
	    			//System.out.println("\nThe ID was not found.");
	                break;
	            //displaying all students
	            case 3:
	            	File sr = new File("StudentReport.txt");
	            	try {
	            		if(sr.createNewFile()) {
	            			System.out.println("Created StudentReport.txt");
	            		}
	            		FileWriter writer = new FileWriter(sr);
	            		Collections.sort(studentList);
	            		for(student stud : studentList) {
		            		System.out.println("\n" + stud.getFirst_name() + " " + stud.getLast_name());
		            		writer.write(stud.getFirst_name() + " " + stud.getLast_name() + "\n");
		            		
		            		
		            		System.out.println("ID: " + stud.getId());
		            		writer.write("ID: " + stud.getId() + "\n");
		            		
		            		System.out.println("Level: " + stud.getLevel());
		            		writer.write("Level: " + stud.getLevel() + "\n\n");
		            		if(stud.getActivity() == true) {
		            			System.out.println("Status: Active\n");
		            		}
		            		else {
		                		System.out.println("Status: Inactive\n");
		            		}
	            		}
	            		writer.close();
	            	}
	            	catch (IOException e) {
	            		e.printStackTrace();
	            	}
	                break;
	            //student activity level 
	            case 4:
	            	Scanner scan3 = new Scanner(System.in);
	            	System.out.print("Enter the student ID: ");
	            	findID = scan3.nextInt();
	            	
	            	for(student stud : studentList) {
	            		if(stud.getId() == findID) {
	            			System.out.println("\n" + stud.getFirst_name() + " " + stud.getLast_name());
	                		System.out.println("ID: " + stud.getId());
	                		System.out.println("Level: " + stud.getLevel());
	                		if(stud.getActivity() == true) {
	                			System.out.println("Status: Active\n");
	                			break;
	                		}
	                		else {
	                    		System.out.println("Status: Inactive\n");
	                    		break;
	                		}
	            		}
	            		
	            	}
	            	break;
	            case 5: 
	            	Scanner scan4 = new Scanner(System.in);
	            	System.out.println("Enter Student ID: ");
	            	findID = scan4.nextInt();
	            	for(student stud : studentList) {
	            		if(stud.getId() == findID) {
	            			String jobChoice = null;
	            			Scanner scan5 = new Scanner(System.in);
	            			boolean valid = false;
	            			do {
		            			System.out.println("Enter job(TA or RA): ");
		            			jobChoice = scan5.nextLine();
		            			switch(jobChoice){
		    	            	case "TA":
		    	            		stud.setJobChoice(jobChoice);
		    	            		valid = true;
		    	            		break;
		    	            	case "RA":
		    	            		stud.setJobChoice(jobChoice);
		    	            		valid = true;
		    	            		break;
		    	            	default:
		    	            		System.out.println("Job is invalid");
		    	            		break;
		    	            	}
	    	            	} while (!valid);
	    	            	System.out.println("Enter job type (part-time or full-time): ");
	    	            	String jobType = scan5.next();
	    	            	valid = false;
	    	            	do {
		    	            	switch(jobType){
		    	            	case "part-time":
		    	            		stud.setJobType(jobType);
		    	            		valid = true;
		    	            		break;
		    	            		
		    	            	case "full-time":
		    	            		stud.setJobType(jobType);
		    	            		valid = true;
		    	            		break;
		    	            	default:
		    	            		System.out.println("Job type is invalid");
		    	            		break;
		    	            	}
	    	            	} while (!valid);
	    	           
	    					System.out.println(stud.getFirst_name() + " " + stud.getLast_name() + " has been assigned a " + stud.getJobType() + " " 
	    					+ stud.getJobChoice() + " job.");
	      
	            		}
	            	}
	                break;

	            case 6: 
	            	// sort list for students only with jobs
	                 for(student stud : studentList) {
	                	 if(stud.isWorking())
		            		System.out.println("\n" + stud.getFirst_name() + " " + stud.getLast_name());
		            		System.out.println("\nID - " + stud.getId());
		            		System.out.println(stud.getJobChoice() + " " + stud.getJobType());
	                 }
	                 break;
	            default:
	                //System.out.println("Invalid response !!");
	                 break;
		        }
				}while(choice != 0);
			
			case 2:
				//***Welcome to CMS***
				//Press ‘1’ to add a new course
				//Press ‘2’ to assign student a new course
				//Press ‘3’ to display student with assigned courses
				//Press ‘0’ to exit CMS
				do {
					System.out.println("\nWelcome to Course Management System!");
					System.out.println("Press ‘1’ to add a new course");
					System.out.println("Press ‘2’ to assign student a new course");
					System.out.println("Press ‘3’ to display student with assigned courses");
					System.out.println("Press ‘0’ to exit CMS");
					choice = sc.nextInt();
					int findID;
					switch (choice){
					
					//entering 1
					//Enter course ID: 3311
					//Enter course name: Java 101
					//Confirmation: New course 3311 has been added
					case 1:
						File crs = new File("Courses.txt");
		            	try {
		            		
		            		if(crs.createNewFile()) {
		            			System.out.println("Created Courses.txt");
		            		}
		            		FileWriter writer = new FileWriter(crs, true);
		            		Scanner cms1 = new Scanner(System.in);
		            		System.out.println("Enter course ID: ");
							int courseID = cms1.nextInt();
							writer.write("Course ID: " + courseID);
							
							Scanner cms2 = new Scanner(System.in);
							System.out.println("Enter course name: ");
							String courseN = cms2.nextLine();
							writer.write("\nCourse Name: " + courseN + "\n");
							
		            		writer.close();
		            	}
		            	catch (IOException e) {
		            		e.printStackTrace();
		            	}

						break;
					//entering 2 
					//Enter course ID: 3311
					//Enter course name: Java 101
					//Confirmation: New course 3311 has been added
					case 2:
						Scanner scan5 = new Scanner(System.in);
		            	System.out.println("Enter Student ID: ");
		            	findID = scan5.nextInt();
		            	for(student stud : studentList) {
		            		if(stud.getId() == findID) {
		            			System.out.println("Enter Course ID: ");
		            			int courseID = scan5.nextInt();
		            			//confirmed adding student to course
		    					System.out.println("Confirmation: " + stud.getFirst_name() + " " + stud.getLast_name() + " has been assigned a " + stud.getCourseID());
		      
		            		}
		            	}
						break;
					//entering 3 
					//Joe Smith 
					//ID – 7 
					//Courses: 3311 
					case 3:
						 for(student stud : studentList) {
		                	 if(stud.hasCourse())
			            		System.out.println("\n" + stud.getFirst_name() + " " + stud.getLast_name());
			            		System.out.println("\nID - " + stud.getId());
			            		System.out.println("Courses: " + stud.getCourseID());
		                 }
		                 break;
						
					//entering 0 returns the main system
					default:
						break;
						}
					} while (choice != 0);
				break;
				}
			}while(choice != 1 || choice != 2);
		System.out.println("Good Bye!");
	}
