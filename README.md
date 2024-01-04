PROJECT:= Create an OOP Based System for Storing School Data Using Design Patterns

Code:==

using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace SchoolDataSystem
{

    // Interface for Student
    public interface IStudent
    {
        string Name { get; set; }
        string ClassAndSection { get; set; }
    }

    // Interface for Teacher
    public interface ITeacher
    {
        string Name { get; set; }
        string ClassAndSection { get; set; }
    }

    // Interface for Subject
    public interface ISubject
    {
        string Name { get; set; }
        string SubjectCode { get; set; }
        ITeacher AssignedTeacher { get; set; }
    }

    // Concrete implementation for Student
    public class Student : IStudent
    {
        public string Name { get; set; }
        public string ClassAndSection { get; set; }
    }

    // Concrete implementation for Teacher
    public class Teacher : ITeacher
    {
        public string Name { get; set; }
        public string ClassAndSection { get; set; }
    }

    // Concrete implementation for Subject
    public class Subject : ISubject
    {
        public string Name { get; set; }
        public string SubjectCode { get; set; }
        public ITeacher AssignedTeacher { get; set; }
    }


    // Singleton pattern for data store
    public class SchoolDataStore
    {
        private static SchoolDataStore instance;

        private SchoolDataStore() { }

        public static SchoolDataStore Instance
        {
            get
            {
                if (instance == null)
                {
                    instance = new SchoolDataStore();
                }
                return instance;
            }
        }

        // Lists to store students, teachers, and subjects
        public List<IStudent> Students { get; set; } = new List<IStudent>();
        public List<ITeacher> Teachers { get; set; } = new List<ITeacher>();
        public List<ISubject> Subjects { get; set; } = new List<ISubject>();
    }



    // Factory pattern for creating objects
    public class SchoolFactory
    {
        public static IStudent CreateStudent(string name, string classAndSection)
        {
            return new Student { Name = name, ClassAndSection = classAndSection };
        }

        public static ITeacher CreateTeacher(string name, string classAndSection)
        {
            return new Teacher { Name = name, ClassAndSection = classAndSection };
        }

        public static ISubject CreateSubject(string name, string subjectCode, ITeacher assignedTeacher)
        {
            return new Subject { Name = name, SubjectCode = subjectCode, AssignedTeacher = assignedTeacher };
        }
    }



    class Program
    {
        static void Main()
        {
            // Fill data using Factory
            var student = SchoolFactory.CreateStudent("Student1", "Class A");
            var teacher = SchoolFactory.CreateTeacher("Teacher1", "Class S");
            var subject = SchoolFactory.CreateSubject("Math", "M101", teacher);

            // Add objects to the data store
            SchoolDataStore.Instance.Students.Add(student);
            SchoolDataStore.Instance.Teachers.Add(teacher);
            SchoolDataStore.Instance.Subjects.Add(subject);

            // Display data
            Console.WriteLine($"Students in {student.ClassAndSection}: {student.Name}");
            Console.WriteLine($"Subjects taught by {teacher.Name}: {subject.Name} (Code: {subject.SubjectCode})");

        }
    }
}




