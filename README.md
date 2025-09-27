#include <iostream>
#include <string>
using namespace std;

// 부모 클래스 (기반 클래스)
class Person {
protected:
    string name;
    int age;

public:
    Person(string n, int a) : name(n), age(a) {}
    void introduce() {
        cout << "이름: " << name << ", 나이: " << age << endl;
    }
   //public 함수를 추가하여 private함수를 간접 호출
    void call_introduce2() {
        introduce2(); //같은 클래스 내부이므로 private 함수 호출 가능
    }
private:
    void introduce2() {
        cout << "이름: " << name << ", 나이: " << age << endl;
    }
protected:
    void introduce3() {
        cout << "이름: " << name << ", 나이: " << age << endl;
    }
};

//자식 클래스 ( pyblic )
class Student : public Person {
private:
    string major;

public:
    Student(string n, int a, string m) : Person(n, a), major(m) {}

    void study() {
        cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl;
    }
};
//자식 클래스2 ( private )
class Student2 : private Person {
private:
    string major;

public:
    Student2(string n, int a, string m) : Person(n, a), major(m) {}

    void study() {
        cout << name << " 학생이 " << major << " 전공 공부 중입니다. " << endl;
    }
};
//자식 클래스3 ( protected )
class Student3 : protected Person {
private:
    string major;

public:
    Student3(string n, int a, string m) : Person(n, a), major(m) {}

    void study() {
        cout << name << " 학생이 " << major << " 전공 공부 중입니다." << endl;
    }
};
int main() {
    Student s("홍길동", 21, "컴퓨터공학");
    //ㅡㅡㅡㅡㅡpublicㅡㅡㅡㅡㅡㅡ
    s.introduce();   // 부모 클래스 함수 사용
    s.study();       // 자식 클래스 함수 사용
    //ㅡㅡㅡㅡㅡprivateㅡㅡㅡㅡㅡㅡ
    s.call_introduce2(); //private 함수를 간접 호출
    Student2 s2("홍길동", 21, "컴퓨터공학");
    //s2.introduce2(); // 컴파일 오류
    s2.study();     // 자식 클래스 함수는 호출됨
    //ㅡㅡㅡㅡㅡprotectedㅡㅡㅡㅡㅡ
    Student3 s3("홍길동", 21, "컴퓨터공학");
    //s3.introduce3(); // 컴파일 오류
    s3.study();     // 자식 클래스 함수는 호출됨

    return 0;
}
