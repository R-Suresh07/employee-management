#include <iostream>
#include <vector>
#include <fstream>
using namespace std;
class Employee{
public:
    float salary;
    string name;
    int projects_completed;
    int age;
    int appraisal_score;
    int E_id;
    int working_days;
private:
    friend void display_salary(Employee);
public:
    Employee(){
        name="NULL";
        projects_completed=0;
        salary=0;
        age=0;
        appraisal_score=0;
        E_id=0;
        working_days=0;
    }
    void copy_employee(Employee &E){
        name=E.name;
        projects_completed=E.projects_completed;
        salary=E.salary;
        age=E.age;
        appraisal_score=E.appraisal_score;
        E_id=E.E_id;
        working_days=E.working_days;
    }
    friend ostream & operator << (ostream &out, const Employee &e);
    friend istream & operator >> (istream &in, Employee &e);
    void input(){
        cout<<"Enter the name of the employee"<<endl;
        cin>>name;
        cout<<"Enter the number of projects completed of the employee"<<endl;
        cin>>projects_completed;
        cout<<"Enter the salary of the employee"<<endl;
        cin>>salary;
        cout<<"Enter the age of the employee"<<endl;
        cin>>age;
        cout<<"Enter Appraisal Score of the employee"<<endl;
        cin>>appraisal_score;
        cout<<"Enter Employee ID of the employee"<<endl;
        cin>>E_id;
        cout<<"Enter the number of days the employee has worked"<<endl;
        cin>>working_days;
    }
    void output(){
        cout<<"The name is:"<<name<<endl;
        cout<<"Number of Projects completed is:"<<projects_completed<<endl;
        cout<<"Salary is:"<<salary<<endl;
        cout<<"Age is:"<<age<<endl;
        cout<<"Appraisal Score is:"<<appraisal_score<<endl;
        cout<<"Employee ID is:"<<E_id<<endl;
        cout<<"Days Worked is:"<<working_days<<endl;
    }



};
void display_salary(Employee e){
    cout<<"Salary of the employee is:"<<e.salary<<endl;
}
void operator > (Employee e1,Employee e2){
    if(e1.salary>e2.salary){
        cout<<"First employee has a bigger salary!\n";
    }
    else
        cout<<"Second employee has a bigger salary!\n";
}
ostream & operator << (ostream &out, const Employee &e){
    out<<"The name is:"<<e.name<<endl;
    out<<"Number of Projects completed is:"<<e.projects_completed<<endl;
    out<<"Salary is:"<<e.salary<<endl;
    out<<"Age is:"<<e.age<<endl;
    out<<"Appraisal Score is:"<<e.appraisal_score<<endl;
    out<<"Employee ID is:"<<e.E_id<<endl;
    out<<"Number of Days worked is:"<<e.working_days<<endl;
    out<<endl;
    return out;
}

istream & operator >> (istream &in, Employee &e){
    cout<<"Enter the name of the employee"<<endl;
    in>>e.name;
    cout<<"Enter the number of projects completed of the employee"<<endl;
    in>>e.projects_completed;
    cout<<"Enter the salary of the employee"<<endl;
    in>>e.salary;
    cout<<"Enter the age of the employee"<<endl;
    in>>e.age;
    cout<<"Enter Appraisal Score of the employee"<<endl;
    in>>e.appraisal_score;
    cout<<"Enter Employee ID of the employee"<<endl;
    in>>e.E_id;
    cout<<"Enter the number of days the employee has worked"<<endl;
    in>>e.working_days;
    return in;
}
void Best_employee(Employee A[5]){
    int max_salary=0;
    for(int i=0;i<5;i++){
        if(max_salary<A[i].salary){
            max_salary=A[i].salary;
        }
        cout<<"Salary of Employee "<<i+1<<" is "<<A[i].salary<<endl;
    }
    cout<<"The best salary is:"<<max_salary<<endl;
}
void best_appraisal_score(vector<Employee> E[10]) {
    vector<Employee>::iterator it;
    int max_appraisal = 0;
    int max_id = 0;
    for (it = E->begin(); it != E->end(); it++) {
        if (max_appraisal < it->appraisal_score) {
            max_appraisal = it->appraisal_score;
            max_id = it->E_id;
        }
        cout << "Appraisal Score:" << it->appraisal_score << endl;
    }
    for (it = E->begin(); it != E->end(); it++) {
        if (max_id == it->E_id) {
            cout<<"The best employee is:"<<it->name;

        }
    }
}
void save_employee_name(Employee e){
    ofstream fout("employee_names2.txt",ios::out | ios::app);
    fout<<e.name;
    fout.close();
}
void view_employee_list(){
    ifstream fin("employee_names2.txt");
    string cont;
    fin>>cont;
    cout<<cont;
    fin.close();
}
void save_employee_details(Employee e){
        fstream fs;
        fs.open("Employee_Details2.txt",ios::out | ios::app);
        fs<<e.name<<' '<<e.salary<<' '<<e.E_id<<' '<<e.appraisal_score<<' '<<e.working_days<<' '<<e.age;
        cout<<"Written into file successfully\n";
        fs.close();
        save_employee_name(e);
}
void below_1Lakh(){
    ifstream fin("Employee_Details2.txt",ios::in);
    Employee e;
    while(!fin.eof()) {
        fin >> e.name >> e.salary >> e.E_id >> e.appraisal_score >> e.working_days >> e.age;
        if(e.salary<100000){
            e.output();
        }
    }
}
class Department{
protected:
    string department_name;
    int D_id;
    int employee_num;
    double budget;
public:
    Department(){
        department_name="NULL";
        employee_num=0;
        budget=0;
        D_id=0;
    }
    Department(string department_name,int employee_num,double budget,int D_id){
        this->department_name=department_name;
        this->employee_num=employee_num;
        this->budget=budget;
        this->D_id=D_id;
    }
    void input_Department(){
        cout<<"Enter Department Name:"<<endl;
        cin>>department_name;
        cout<<"Enter number of employees:"<<endl;
        cin>>employee_num;
        cout<<"Enter Department's budget:"<<endl;
        cin>>budget;
        cout<<"Enter Department ID:"<<endl;
        cin>>D_id;
    }

    void display();
    virtual int average_budget()=0;
};
inline void Department::display() {
    cout<<"Name of the Department is:"<<department_name<<endl;
    cout<<"Number of Employees is:"<<employee_num<<endl;
    cout<<"Department budget is:"<<budget<<endl;
    cout<<"Employee ID is:"<<D_id<<endl;
}
const int total_working_Days=240;
class HRDepartment:public Department{
public:
    Employee *e=new Employee[20];
    HRDepartment(){
        input_Department();
    }
    void appraise_Employee(){
        cout<<"Enter the ID of the employee to be appraised";
        int temp_id;
        cin>>temp_id;
        int flag=0;
        for(int i=0;i<employee_num;i++){
            if(e[i].E_id == temp_id){
                flag=1;
                try{
                    if(e[i].projects_completed==0 || e[i].working_days<total_working_Days/2)
                        throw 0;
                    if(e[i].appraisal_score>75 && e[i].projects_completed>2)
                    {
                        e[i].salary=e[i].salary*1.02;
                        cout<<"Employee Appraised Successfully\n";
                    }
                    else if(e[i].appraisal_score>85 && e[i].projects_completed>8)
                    {
                        e[i].salary=e[i].salary*1.03;
                        cout<<"Employee Appraised Successfully\n";
                    }
                    else if(e[i].appraisal_score>90 && e[i].projects_completed>10)
                    {
                        e[i].salary=e[i].salary*1.05;
                        cout<<"Employee Appraised Successfully\n";
                    }
                }catch(int a) {
                    cout<<"Employee has done 0 projects or hasn't worked the minimum amount of days required for an appraisal and can't be appraised\n";
                }
            }
        }
        if(flag==0){
            cout<<"No such ID belongs to an Employee\n";
        }
    }
    void best_employee(){
        int max_appraisal_score=-1;
        int max=-1;
        for(int i=0;i<employee_num;i++){
            if(max_appraisal_score<e[i].appraisal_score){
                max_appraisal_score=e[i].appraisal_score;
                max=i;
            }
        }
        cout<<"Best Employee is:"<<endl;
        e[max].Employee::output();
    }
    void display(){
        Department::display();
        for(int i=0;i<employee_num;i++){
            e[i].output();
        }
    }
    int average_budget() override{
        return budget/employee_num;
    }
    ~HRDepartment(){
        delete[] e;
    }
};
template<class T>
class Array{
public:
    T List[5];
};
int main() {
    int choice=0;
    cout<<"**************************************** EMPLOYEE MANAGEMENT PORTAL ****************************************\n";
    cout<<"ENTER THE OPERATION TO BE PERFORMED\n";
    cout<<"1)SHOWCASE FEATURES OF EMPLOYEE\n";
    cout<<"2)SHOWCASE FEATURES OF DEPARTMENT AND HRDEPARTMENT\n";
    cout<<"3)EXIT\n";
    cin>>choice;
    switch (choice) {
        case 1:
        {
            cout<<"Creating an employee and inputting details:\n";
            Employee e1;
            cin>>e1;
            cout<<"Displaying said employee's Details:\n";
            cout<<e1;
            cout<<"Creating another employee to showcase which employee has a higher salary via operator overloading:\n";
            Employee e2;
            cin>>e2;
            e1>e2;
            cout<<"Creating an array of employee objects using class templates and finding the best employee among them\n";
            Array<Employee> a;
            a.List[0].salary=10000;
            a.List[1].salary=20000;
            a.List[2].salary=30000;
            a.List[3].salary=40000;
            a.List[4].salary=50000;
            Best_employee(a.List);
            cout<<"Using vectors to create a dynamic array of employee objects and finding the employee with the best appraisal score\n";
            vector<Employee> E[10];
            Employee temp;
            temp.name="James";
            temp.appraisal_score=96;
            temp.E_id=101;
            E->push_back(temp);
            temp.name="Mary";
            temp.appraisal_score=48;
            temp.E_id=102;
            E->push_back(temp);
            temp.name="John";
            temp.appraisal_score=59;
            temp.E_id=103;
            E->push_back(temp);
            temp.name="Patricia";
            temp.appraisal_score=22;
            temp.E_id=104;
            E->push_back(temp);
            temp.name="Robert";
            temp.appraisal_score=15;
            temp.E_id=105;
            E->push_back(temp);
            temp.name="Jennifer";
            temp.appraisal_score=69;
            temp.E_id=106;
            E->push_back(temp);
            temp.name="Michael";
            temp.appraisal_score=68;
            temp.E_id=107;
            E->push_back(temp);
            temp.name="Linda";
            temp.appraisal_score=3;
            temp.E_id=108;
            E->push_back(temp);
            temp.name="William";
            temp.appraisal_score=36;
            temp.E_id=109;
            E->push_back(temp);
            temp.name="Elizabeth";
            temp.appraisal_score=77;
            temp.E_id=110;
            E->push_back(temp);//54,43.8
            best_appraisal_score(E);
            cout<<"\nNow lets save some employee details onto a file\n";
            cout<<"This is the state of the File before you have saved the employee's name\n";
            view_employee_list();
            save_employee_details(e1);
            cout<<"And this is the state of the File after you have saved the employee's name\n";
            view_employee_list();
            break;
        }
        case 2:
        {
            cout<<"\n Lets Start out by creating a HRDepartment Object and initialising it some values\n";
            HRDepartment h;
            Employee e1,e2,e3;
            e1.name="Rem";
            e1.salary=34000;
            e1.age=19;
            e1.E_id=111;
            e1.appraisal_score=92;
            e1.working_days=291;
            e1.projects_completed=12;
            e2.name="Betty";
            e2.salary=45000;
            e2.age=21;
            e2.E_id=112;
            e2.appraisal_score=78;
            e2.working_days=312;
            e2.projects_completed=0;
            e3.name="Emilia";
            e3.salary=99000;
            e3.age=21;
            e3.E_id=113;
            e3.appraisal_score=94;
            e3.working_days=110;
            e3.projects_completed=20;
            h.e[0]=e1;
            h.e[1]=e2;
            h.e[2]=e3;
            cout<<"Let's Display some of the objects i have prepared in advance\n";
            h.display();
            cout<<endl;
            cout<<"Now lets do some employee appraisal on these employees\n";
            h.appraise_Employee();
            h.appraise_Employee();
            h.appraise_Employee();
            cout<<"Now lets find the employee with the best appraisal score of them all \n";
            h.best_employee();
            cout<<"Lets find the average budget of the department which is possible via function overriding:";
            cout<<h.average_budget();
            break;
        }
        case 3:
        {
            exit(0);
            break;
        }
        default:
            cout<<"Please Enter Only the above choices\n";

    }
    return 0;
}