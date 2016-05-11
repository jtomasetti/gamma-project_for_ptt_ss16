#  Summary
This repo is conceptually part of [101repo](http://101companies.org/wiki/).

This repo contains Java-based contributions that are easy to build, run, and test.

The physical location of this repo is here:

[https://github.com/jtomasetti/gamma-project_for_ptt_ss16_ass01](https://github.com/jtomasetti/gamma-project_for_ptt_ss16_ass01)

The master ZIP file for the repo is this one:

[https://github.com/jtomasetti/gamma-project_for_ptt_ss16_ass01/ppt_ss16_gamma_ass01.zip](https://github.com/jtomasetti/gamma-project_for_ptt_ss16_ass01/ppt_ss16_gamma_ass01.zip)

This is the First Assignment of group "gamma" of course "Programming techniques and technologies" in SS 2016

Description of the project can be found in the 101companies-wiki:

http://101companies.org/wiki/Contribution:JavaFXFlatcompany

# Prerequisites

[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

[e(fx)clipse](http://efxclipse.bestsolution.at/install.html#all-in-one)

[scene builder 8.0](http://gluonhq.com/open-source/scene-builder/)

# Usage:

  To run the programm, just run https://github.com/jtomasetti/gamma-project_for_ptt_ss16_ass01/ContributionJavaFXFlatCompany.jar.
  
  To view the code import ppt_ss16_gamma_ass01.zip into e(fx)clipse.
  
# Characteristics

The contribution has many features to allow easy administration of the [101company](http://101companies.org/wiki/101company). Firstly you are able to create new employees with several attributes by using the new Button. The code for this button is created by the author of the [tutorial](http://code.makery.ch/library/javafx-8-tutorial/part1/::tutorial)  (name: Marco Jakob) but we put a line in the handleNew function ( mainApp.setSavedData(mainApp.getPersonData()); ) to save the “State” for the  [Undo-function](http://101companies.org/wiki/Feature:Undo-redo) and to implement our design pattern [Memento](https://en.wikipedia.org/wiki/Memento). The before-mentioned line is also used in the [Feature:Editing](http://101companies.org/wiki/Feature:Editing) and [Feature:Cut](http://101companies.org/wiki/Feature:Cut).

By using the “Edit”-feature, the data of a selected employee can be changed.

The [Feature:Total](http://101companies.org/wiki/Feature:Total) calculates the total salaries of the employees.

The feature “Cut” divides the salary of each employee by two.

The [Feature:Median](http://101companies.org/wiki/Feature:Median) calculates the median of the salaries of the employees . 

Including the case that an employee leaves the company, you are able to remove him from the list by using the "Delete"-feature.

Last but not least you can [undo](http://101companies.org/wiki/Feature:Undo-redo) your actions or mistakes by using the “undo”-button. It is designed by us using the Memento pattern. There are also functions for saving (/save as) your file as an XML-data file [Serialization](http://101companies.org/wiki/Serizalation). You can open saved projects or create a new one. They are  implemented by the author in the tutorial Marco Jakob and token over into the code. Group gamma wants to thank him at this point for his tutorial and help with the code.

# Motivation

By using our contribution, one could easily administrate the information about the employees of a [Flat company](http://101companies.org/wiki/Flat company.) The features are simple to execute by using the interface’s buttons and mistakes can instantly be fixed by using the undo-button. It is also made for long time usage by including a [Feature:History](http://101companies.org/wiki/Feature:History) and an option for saving. 

# Features

Feature „Edit“:

    @FXML
    private void handleEditPerson()

Feature „Total“:

    @FXML
    private void handleTotal() {
    	double total = 0; int i=0;
    	ObservableList<Employee> employeeList = mainApp.getPersonData();
    	int max = employeeList.size();
    	while(i<max) {
    		total += employeeList.get(i).getSalary();
    		i++;
    	}
    	totalLabel.setText(Double.toString(total));
    }
Feature “Cut”:

    @FXML
    private void handleCut() {
      	mainApp.setSavedData(mainApp.getPersonData());
      	ObservableList<Employee> employeeList = mainApp.getPersonData();
    	Iterator<Employee> iter = employeeList.iterator();
    	Employee employee = iter.next();
    	while(employee != null) {
    		employee.setSalary(employee.getSalary()/2);
    		employee = iter.next();
    	}    	
    }
Feature “Median”:

    @FXML
    private void handleMedian() {
    	ObservableList<Employee> unsort = FXCollections.observableArrayList();
    	ObservableList<Employee> employeeList= mainApp.getPersonData();
    	EmployeeListWrapper wrapper = new EmployeeListWrapper();
        wrapper.setPersons(mainApp.getPersonData());
     	unsort.clear();
    	unsort.addAll(wrapper.getPersons());
    	int n = employeeList.size();double median;
    	quicksort(0,n-1,employeeList); // sortiert die Employee-Daten
    	if(n%2==0) {
    		median = (employeeList.get(n/2).getSalary()+employeeList.get((n/2)-1).getSalary())/2; 
    	} else {
    		median = employeeList.get((n/2)).getSalary();
    	}
    	wrapper = new EmployeeListWrapper();
        wrapper.setPersons(unsort);
     	mainApp.personData.clear();
    	mainApp.personData.addAll(wrapper.getPersons());
    	medianLabel.setText(Double.toString(median));
    }
Feature “Undo”:

    @FXML
    private void undo() {
    		mainApp.restorePersonData(mainApp.getSavedData());    	
    }

  
