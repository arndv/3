# 4

Обяснете основните разлики между презареждане и презаписване на методи.

Методи с едно и също име, но различни сигнатури. [Презареждане на методи]
Може да се случи в същия клас или в негов подклас. [Презареждане на методи]
Може да се случи в подкласовете. [Презаписване на методи]
Трябва да има същия тип на връщана стойност. [Презаписване на методи]
При компилиране, според подадените параметри компилатора определя кой метод точно ще изпълни. [Презареждане на методи]
Модификатора за достъп не може да бъде по-ограничаващ. [Презаписване на методи]



Посочете кое е другото название, с което наричаме шаблонните класове в C#.

Generics

-----------------------------------------------------------------------------------------------------------

Дайте пример за шаблонен клас, който да се казва Кутия и тази кутия да може да съхранява всичко. В този клас създайте и един метод, който да добавя елемент в края на редицата.

class Box<T>
    {
        private List<T> items;

        public Box()
        {
            items = new List<T>();  
        }
        public void Add(T item)
        {
            this.items.Add(item);
        }
    }

-------------------------------------------------------------------------------------------------------------------------

Дайте пример за абстракция. Напишете примерен код, който:

Има класовете BaseEmployee, FullTimeEmployee и ContractEmployee.

Условието на задачата е всички работници да имат име, както и  метод CalculateSalary(int workingHours) - който ще изчислява заплатата за работника, като се приема параметър – брой изработени часове. 

Заплатата на FullTimeEmployee се изчислява по формулата: 250 + workingHours*10.80.

А заплатата на ContractEmployee по формулата: 250 + workingHours*20.

Спазвайте принципа за абстракция в обектно-ориентираното програмиране.

abstract class BaseEmployee
    {
        public string Name { get; set; }
        public abstract double CalculateSalary(int workingHours);
    }

    class FullTimeEmployee : BaseEmployee
    {
        public override double CalculateSalary(int workingHours)
        {
            return 250 + workingHours * 10.80;
        }
    }

    class ContractEmployee : BaseEmployee
    {
        public override double CalculateSalary(int workingHours)
        {
            return 250 + workingHours * 20;
        }
    }

--------------------------------------------------------------------------------------------------------------------------
Посочете какви са приликите и разликите между полиморфизъм и абстракция в обектно-ориентираното програмиране като поставите липсващите думи в текста.

Полиморфизмът може много да напомня на абстракцията, но в програми­рането се свързва най-вече с [пренаписването (override) ] на методи в [нас­ледените класове] с цел [промяна на оригиналното им поведение], насле­дено от базовия клас. Абстракцията се свързва със [създаването на интерфейс на компонент] или функционалност.

----------------------------------------------------------------------------------------------------------------------------
Свържете кои от характеристиките се отнасят за абстрактните класове, кои за интерфейсите.

Може да притежава полета и константи. [Абстрактни класове]

Е по-добър избор, ако множество имплементации споделят само сигнатурата на методите и нищо друго. [Интерфейси]

Не поддържа полета. [Интерфейси]

Е по-добър избор, ако множество имплементации са от сходен вид и имат общо поведение или статут. [Абстрактни класове]

Ако добавим нов метод, то имаме опцията да създадем имплементация по подразбиране и така съществуващият код ще може да работи коректно. [Абстрактни класове]

Ако добавим нов метод, то трябва да проследим всичките му имплементации и да дефинираме имплементация за новия метод. [Интерфейси]

------------------------------------------------------------------------------------------------------------------------
Създайте следната йерархия от класове и интерфейси.

abstract class Animal : IAnimal

    {

        private string name;

 

        protected Animal(string name)

        {

            Name = name;

        }

 

        public string Name

        {

            get { return name; }

            private set

            {

                if (string.IsNullOrEmpty(value) || string.IsNullOrWhiteSpace(value))

                {

                    throw new ArgumentException("Name can't be null or empty!");

                }

                name = value;

            }

        }

 

        public string Type {  }

       

        public void Perform()

        {

            Console.WriteLine($">>> {this.MakeNoise()}");

            Console.WriteLine($">>> {this.MakeTrick()}");

        }

 

        public override string ToString()

        {

            return base.ToString();

        }

    }

class Cat

    {

        public Cat(string name) : base(name)

        {

        }

 

        public override string MakeNoise()

        {

           

        }

 

        public override string MakeTrick()

        {

           

        }

 

    }

class Dog

    {

        public Dog(string name) : base(name)

        {

        }

 

        public override string MakeNoise()

        {

           

        }

 

        public override string MakeTrick()

        {

           

        }

    }


interface IAnimal

    {

        public string Type  get; }

        public string Name { get; }

        void Perform();

    }


interface IMakeNoise

    {

        string MakeNoise();

    }


interface IMakeTrick

    {

        string MakeTrick()

    }

class Program

    {

        static void Main(string[] args)

        {

            List<Cat> animals = new List<Cat>();

 

            int n = int.Parse(Console.ReadLine());

 

            for (int i = 0; i < n; i++)

            {

                string[] line = Console.ReadLine().Split();

                IAnimal animal = CreateAnimal(line);

                animals.Add(animal);

            }

 

            string trainerName = Console.ReadLine();

 

            Trainer trainer = null;

 

            string name = Console.ReadLine();

 

            while (name != "End")

            {

                IAnimal current = animals.Where(a => a.Name.Equals(name)).FirstOrDefault();

 

                if (current == null)

                {

                    Console.WriteLine("No such name in the Database!");

               

                else

                {

                    if (trainer == null)

                    {

                        trainer = new Trainer(trainerName, current);

                    }

                    trainer.Work(current);

                    trainer.Make();

                }

 

            }

        }

        private static IAnimal CreateAnimal(string[] line)

        {

            IAnimal animal = null;

            switch (line[0])

            {

                case "Cat":

                    animal = new Cat(line[1]);

                    break;

                case "Dog":

                    animal = new Dog(line[1]);

                    break;

            }

            return animal;

        }

    }

Trainer

    {

        private IAnimal entity;

        private string name;

 

        public Trainer(string name, IAnimal entity)

        {

            this.Name = name;

            this.Entity = entity;

        }

 

        public string Name

        {

            private set

            {

                if (string.IsNullOrEmpty(value) || string.IsNullOrWhiteSpace(value))

                {

                    throw new ArgumentException("Name can't be null or empty!");

                }

                name = value;

            }

        }

        public IAnimal Entity

        {

            get { return Еntity; }

            private set

            {

                entity = value;

            }

        }

 

        public void Work(IAnimal entity)

        {

            this.Entity = entity;

            Console.WriteLine($"Trainer {this.Name} works with {Entity}!");

        }

 

        public void Make()

        {

            this.Entity.Perform();

        }

    }

---------------------------------------------------------------------------------------------------------------------

Посочете кое от изброените твърдение е вярно за класовете в C#.


Можем да създаваме инстанции., Описва състоянието и поведението на обектите
  
  --------------------------------------------------------------------------------------------------------------------
  
  Открийте липсващите думи в текста:
  
  Възможността референция към [базов клас ] да сочи обект както от базовия, така и обект от някой от производните класове е в основата на реализацията на [полиморфизма ] в езика C#.

Кои от следните примери потвърждават това правило, ако имате следната йерархия class Cat : class Animal ?

Cat cat  = new Animal(); [не]

Animal animal = new Animal(); [да]

Animal animal = new Cat(); [да]

------------------------------------------------------------------------------------------------------
  
  Посочете по какъв начин указваме на даден метод от базовия клас, че искаме да презапишем неговото поведение.
  
  Чрез ключовата дума virtual.
  
  -------------------------------------------------------------------------------------------------------------
  
Дайте пример чрез код на C# за това как и къде бихте използвали презаписване на методи. 

 class Animal
{
        public virtual void MakeTrick()
        {
            Console.WriteLine("No trick...");
        }
}
class Dog : Animal
{
        public override void MakeTrick()
        {
            Console.WriteLine("Give a paw...");
        }
}

-------------------------------------------------------------------------------------------------------------
  
  Свържете кои от характеристиките се отнасят за абстракцията, кои за енкапсулацията.
  
  Получава се чрез модификаторите за достъп (private, public, protected, internal) [Енкапсулация]

Постига се чрез интерфейси и абстрактни класове. [Абстракция]

Процес на скриване на подробностите на имплементацията и показване само на функционалностите към потребителя. [Абстракция]

Използва се, за  да скрива кода и информацията в един компонент, за да я защити от външния свят. [Енкапсулация]

---------------------------------------------------------------------------------------------------------------------------
  
 Посочете кое от изброените твърдение е вярно за интерфейсите в C#.
  
  Предоставя договор, определящ как да се създаде обект, без да се интересува от спецификата на това как обекта ще прави нещата., Това е референтен тип и включва само абстрактни членове като събития, методи, свойства и т.н. и няма реализации за нито един от своите членове.
  
---------------------------------------------------------------------------------------------------------------------  
  
  Избройте четирите основни принципа на обектно-ориентираното програмиране.
  
  капсулация, наследяване, абстракция, полиморфизъм
  
  ---------------------------------------------------------------------------------------------------------------------
  
  Дефинирайте понятието полиморфизъм в обектно-ориентираното програмиране като попълните липсващите думи в текста.
  
  Полиморфизмът в обектно-ориентираното програмиране представлява свойството на обектите от един и същи [тип] да имат един и същи [интерфейс], но с [различна реализация] на този [интерфейс]. „Един [интерфейс], [множество от различни реализации]“. Чрез полиморфизма се постига по-голяма [абстракция ] и по-лесно [повторно използване] на кода.

-----------------------------------------------------------------------------------
  
  Дефинирайте термина полиморфизъм в обектно-ориентираното програмиране, като поставите липсващите думи в текста.
  
  Терминът полиморфизъм в обектно-ориентираното програмиране определя, че [едни и същи (еднотипни)] действия се реализират по [различен начин] в зависимост от обектите, върху които се прилагат. Такива действия се наричат [полиморфични]. За да се реализира [полиморфно действие], класовете на обектите, върху които се прилага това действие, трябва да имат [общ корен] т.е. да бъдат производни на [един и същи клас].
  
  -----------------------------------------------------------------------------------------------------------------------
  
  Имате следния код:

        public List<int> CreateList(int item, int count)
        {
            List<int> list = new List<int>();
            for (int i = 0; i < count; i++)
            {
                list.Add(item);
            }
        }

 Модифицирайте кода,така че методът да работи с всякакъв тип данни.
  
  public List<T> CreateList<T>(T item, int count)//2т
        {
            List<T> list = new List<T>();//2т
            for (int i = 0; i < count; i++)
            {
                list.Add(item);
            }
            return list;//2т
        }
  
  --------------------------------------------------------------------------
  
  Свържете кои от характеристиките се отнасят за абстрактните класове, кои за интерфейсите.
  
  Може да наследи само един абстрактен клас. [Абстракция]

Могат да предоставят целия код и/или само детайлите, които трябва да се презапишат. [Абстракция]

Може да имплементира няколко интерфейса. [И за двете ]

Може да съдържа модификатори за достъп. [Абстракция]

Не може да предоставя никакъв код, предоставя само описание. [Интерфейси]                        

Нямат модификатори за достъп. Всичко е публично по подразбиране. [Интерфейси]

  ----------------------------------------------
  
  ------------------------------------------
  
  ----------------------------------------------
  
  Дайте пример чрез код на C# за това как и къде бихте използвали презареждане на методи. 
  
   class MathOperations
    {
        public int Add(int a, int b)
        {
            return a + b;   
        }
        public int Add(int a, int b,int c)
        {
            return a + b + c;
        }
    }
  
  -----------------------------------------------------------------------------------------
  
  Посочете кое от изброените твърдение е вярно за класовете в C#.
  
  Можем да създаваме инстанции., Описва състоянието и поведението на обектите
  
  -----------------------------------------------------------------------------------------
  
  Имате абстрактен клас и обикновен клас. Открийте и свържете коя от характеристиките се отнася за абстрактния клас и коя за не абстрактен клас.
  
  Не можем да създаваме инстанции. [Абстрактен клас ]

Може да има само абстрактни членове на класа. [За нито един от двата]

Могат да дефинират методи без тяло (без имплементация). [Абстрактен клас ]

Можем да създаваме инстанции. [Обикновен клас]

Може да има само не-абстрактни членове на класа. [Обикновен клас]

Не могат да дефинират методи без тяло (имплементация). [Обикновен клас]

Съдържа ключовата дума abstract пред ключовата дума class. [Абстрактен клас ]

Може да има абстрактни и не-абстрактни членове на класа. [Абстрактен клас ]

Не съдържа ключовата дума abstract пред ключовата дума class. [Обикновен клас]
  
  ----------------------------------------------------------------------------------------
  
  По време на теоретичния изпит се предоставя непълен/неработещ/некоректен програмен фрагмент. Предоставеният фрагмент да се приведе в работещ вид.
  
  
  internal class Citizen : Community

    {

        private string birthdate;

       

 

        public string Birthdate { get => this.birthdate; set => this.birthdate = value; }

 

        public void BuyFood()

        {

            base.Food += 10;

        }

 

        public override string ToString()

        {

            return base.ToString() + $"Birthdate {this.Birthdate} Food: {base.Food}";

        }

    }
  
  
  
internal abstract class Community : IIdentifiable, IPersonable, IBuyer

    {

        private string id;

        private string name;

        private int age;

        private int food;

        protected Community(string id, string name, int age)

        {

            Id = id;

            Name = name;

            Age = age;

        }

 

        public string Id { get => this.id; set { this.id = value; } }

 

        public string Name => throw new NotImplementedException();

 

        public int Age { get => this.age; set { this.age = value; } }

 

        public int Food { get => this.food; protected set => this.food = value; }

 

 

        public void BuyFood();

 

        public override string ToString()

        {

            return $"ID:{this.Id} {this.GetType().Name} Name: {this.Name} Age {this.Age} ";

        }

    }
  
  
  internal interface IBuyer

    {

        void BuyFood();

        int Food { get; }

    }
  
  
  
internal interface IIdentifiable

   

        string Id { get; }

    }
  
  
  internal class Program

    {

        static void Main(string[] args)

        {

            int n = int.Parse(Console.ReadLine());          

 

            for (int i = 0; i > n; i++)

            {

                string[] input = Console.ReadLine().Split();

                if (community.ContainsKey(input[0]))

                {

                    Community entity = CreateEntity(input);

                    community.Add(input[0], entity);

                }

            }

 

            string id = Console.ReadLine();

            while (true)

            {

                if (community.ContainsKey(id))

                {

                    community[id].BuyFood();

                    Console.WriteLine(community[id]);

                }

                else

                {

                    Console.WriteLine($"Entity with {id} does not exist!");

                }

                id = Console.ReadLine();

            }

            int totalFood = community.Sum(v => v.Value.Food);

            Console.WriteLine("TotalFood: {totalFood}");

        }

 

        public static Community CreateEntity(string[] info)

        {

            Community entity = null;

            string id = info[0];

            if (id.StartsWith("R"))

            {

                entity = new Rebel(id, info[1], int.Parse(info[2]), info[3]);

            }

            else if (id.StartsWith("C"))

            {

                entity = new Citizen(id, info[1], int.Parse(info[2]), info[3]);

            }

            return entity;

        }

    }
  
  
  
internal class Rebel : Community

    {

        private string group;

 

 

        public void BuyFood()

        {

          

        }

 

        public override string ToString()

        {

            return base.ToString() + $"Group {this.Group} Food: {base.Food}";

        }

    }
  
  -----------------------------------------------------------------------------
  
  Свържете кои от характеристиките се отнасят за абстрактните класове, кои за интерфейсите.
  
  Може да притежава полета и константи. [Абстрактни класове]

Е по-добър избор, ако множество имплементации споделят само сигнатурата на методите и нищо друго. [Интерфейси]

Не поддържа полета. [Интерфейси]

Е по-добър избор, ако множество имплементации са от сходен вид и имат общо поведение или статут. [Абстрактни класове]

Ако добавим нов метод, то имаме опцията да създадем имплементация по подразбиране и така съществуващият код ще може да работи коректно. [Абстрактни класове]

Ако добавим нов метод, то трябва да проследим всичките му имплементации и да дефинираме имплементация за новия метод. [Интерфейси]
  
  --------------------------------------------------------------------------------------
  
  Имате зададена следната схема:
  
  ![download](https://github.com/arndv/4/assets/125039034/c4f6130b-d655-4ca4-8c44-0e3f097b28cc)

  Методът ExplainMyself ще бъде презаписан или презареден? 
  
  Методът ще бъде презаписан, защото се използва в подкласовете и има една и съща сигнатура.
    
    
    -------------------------------------------------------------------------------------
  
  
  Имате следния код:

    public class Scale : IComparable
    {
        private var left;
        private var right;

        public Scale(var left, var right)
        {
            this.left = left;
            this.right = right;
        }
        public var GetHavier()
        {
            if (left.CompareTo(right) > 0)
            { return left; }
            else if (left.CompareTo(right) < 0)
            { return right; }
            return default;
        }
    }

Модифицирайте кода,така че Везната да може да сравнява всякакви типове данни. Също така трябва да ограничите Везната, че елементите, които ще  сравнява ще бъдат само сравними типове. 
  
  
  public class Scale<T> where T : IComparable<T>//2т
    {
        private T left; //1т
        private T right; //1т

        public Scale(T left, T right)//2т
        {
            this.left = left;
            this.right = right;
        }
        public T GetHavier()
        {
            if (left.CompareTo(right) > 0)
            { return left; }
            else if (left.CompareTo(right) < 0)
            { return right; }
            return default(T);
        }
    }
  
  --------------------------------------------------------------------------------------------
  
  Посочете видовете полиморфизъм в .NET.
  
  Полиморфизъм по време на компилиране., Полиморфизъм по време на изпълнение. 
  
  -------------------------------------------------------------------------------------------
  
  Посочете видовете полиморфизъм в .NET.
  
  Статичен., Динамичен.
  
  ---------------------------------------------------------------------------------------------
  
  Посочете в кой от случаите бихте използвали шаблонни класове?
  
  Когато се налага да се създават класове, които са сходни по функционалност, а се различават само по типа на обектите, с които работят.
  
  -----------------------------------------------------------------------------------------------
  
  Имате даден следния код:

![download](https://github.com/arndv/4/assets/125039034/94bc2167-8123-4dda-a77c-1547f0a2c348)

Опишете кой от видовете полиморфизъм е използван в примера по-горе.

Полиморфизъм по време на изпълнение.
  
  -------------------------------------------------------------------------------------
  
  Дайте пример за шаблонен клас, който да се казва Кутия и тази кутия да може да съхранява всичко. В този клас създайте и един метод, който да проверява и връща като резултат дали даден елемент се съдържа в тази кутия.
  
  class Box<T>
    {
        private List<T> items;

        public Box()
        {
            items = new List<T>();  
        }

        public bool Contains(T item)
        {
            return this.items.Contains(item);
        }
}
  
  ------------------------------------------------------------------------------------------------------------
    
    Посочете кое от изброените твърдение е вярно за интерфейсите в C#.
    
    Предоставя договор, определящ как да се създаде обект, без да се интересува от спецификата на това как обекта ще прави нещата., Това е референтен тип и включва само абстрактни членове като събития, методи, свойства и т.н. и няма реализации за нито един от своите членове.
    
    -----------------------------------------------------------------------------------------
    
    Открийте разликите между клас и интерфейс. Кои от изброените твърдения се отнасят за класовете в C#, кои за интерфейсите?
    
    Има както дефиниция, така и реализация. [Клас]

Има само дефиниция. [Интерфейс]

Не може да бъде инстанциран. [Интерфейс]

Може да бъде инстанциран. [Клас]

Може да съдържа членове, методи, заедно с дефиниция и реализация. [Клас]

Набор от дефиниции, които трябва да се приложат. [Интерфейс]
    
    ---------------------------------------------------------------------------------------------
    
    Посочете по какъв начин в C# можем да укажем, че искаме да подменим (препокрием) виртуален метод.
    
    Чрез ключовата дума override поставена на методи в наследниците.
    
    ------------------------------------------------------------------------------------------------
    
    Дефинирайте понятието наследяване от обектно-ориентираното програмиране като попълните липсващите думи в текста.
    
    Наследяването е [основен принцип] от обектно-ориентираното програми­ране. То позволява на един клас да "наследява" [поведение и характе­ристики] от друг, по-общ клас. 

    ----------------------------------------------------------------------------------------------------------------
    
В .NET и други модерни езици за програмиране един клас може да наследи [само един друг клас].


Класът, който [дава ] своите членове на [дъщерния] си клас се нарича [базов] клас. А класът, който [получава] членове от [своя базов клас] - [подклас].
    
    --------------------------------------------------------------------------------------------------------------
    
    ---------------------------------------------------------------------------------------------------------
    
    --------------------------------------------------------------------------------------------------------------
    
    Имате следния код:

    public class Scale : IComparable
    {
        private var left;
        private var right;

        public Scale(var left, var right)
        {
            this.left = left;
            this.right = right;
        }
        public var GetHavier()
        {
            if (left.CompareTo(right) > 0)
            { return left; }
            else if (left.CompareTo(right) < 0)
            { return right; }
            return default;
        }
    }

Модифицирайте кода,така че Везната да може да сравнява всякакви типове данни. Също така трябва да ограничите Везната, че елементите, които ще  сравнява ще бъдат само сравними типове. 
    
    public class Scale<T> where T : IComparable<T>//2т
    {
        private T left; //1т
        private T right; //1т

        public Scale(T left, T right)//2т
        {
            this.left = left;
            this.right = right;
        }
        public T GetHavier()
        {
            if (left.CompareTo(right) > 0)
            { return left; }
            else if (left.CompareTo(right) < 0)
            { return right; }
            return default(T);
        }
    }
    
    ---------------------------------------------------------------------------------------------------------------------
    
    Дефинирайте понятието абстракция в обектно-ориентираното програмиране.
    
    Абстракцията означава да работим с нещо, което знаем как да използваме, но не знаем как работи вътрешно.

Абстракцията е действие, при което игнорираме всички детайли, които не ни интересуват от даден обект, и разглеждаме само детайлите, които имат значение за проблема, който решаваме.

Абстракцията ни позволява да пишем код, който работи с абстрактни струк­тури от данни (например списък, речник, множество и други). Имайки абстрактния тип данни, ние можем да работим с него през неговия интер­фейс, без да се интересуваме от имплементацията му.

Има два начина за постигане на абстракция:
Интерфейси (100% абстракция)
Абстрактен клас (0% - 100% абстракция)
    
    -----------------------------------------------------------------------------
    
    Посочете кое от изброените е дефиниция на метод, който може да бъде презаписан в клас наследник.
    
    Виртуален метод.
    
    ---------------------------------------------------------------------------------
    
    Дайте пример чрез код на C# за това как и къде бихте използвали презареждане на методи. 
    
     class MathOperations
    {
        public int Add(int a, int b)
        {
            return a + b;   
        }
        public int Add(int a, int b,int c)
        {
            return a + b + c;
        }
    }
    
    -------------------------------------------------------------------------
    
    Свържете кои от характеристиките се отнасят за абстракцията, кои за енкапсулацията.
    
    Получава се чрез модификаторите за достъп (private, public, protected, internal) [Енкапсулация]

Постига се чрез интерфейси и абстрактни класове. [Абстракция]

Процес на скриване на подробностите на имплементацията и показване само на функционалностите към потребителя. [Абстракция]

Използва се, за  да скрива кода и информацията в един компонент, за да я защити от външния свят. [Енкапсулация]

-----------------------------------------------------------------------------------------
    
    По време на теоретичния изпит се предоставя непълен/неработещ/некоректен програмен фрагмент. Предоставеният фрагмент да се приведе в работещ вид.
    
    
    internal class Citizen : Community

    {

        private string birthdate;

       

 

        public string Birthdate { get => this.birthdate; set => this.birthdate = value; }

 

        public void BuyFood()

        {

            base.Food += 10;

        }

 

        public override string ToString()

        {

            return base.ToString() + $"Birthdate {this.Birthdate} Food: {base.Food}";

        }

    }
    
    
    internal abstract class Community : IIdentifiable, IPersonable, IBuyer

    {

        private string id;

        private string name;

        private int age;

        private int food;

        protected Community(string id, string name, int age)

        {

            Id = id;

            Name = name;

            Age = age;

        }

 

        public string Id { get => this.id; set { this.id = value; } }

 

        public string Name => throw new NotImplementedException();

 

        public int Age { get => this.age; set { this.age = value; } }

 

        public int Food { get => this.food; protected set => this.food = value; }

 

 

        public void BuyFood();

 

        public override string ToString()

        {

            return $"ID:{this.Id} {this.GetType().Name} Name: {this.Name} Age {this.Age} ";

        }

    }
    
    
    
internal interface IBuyer

    {

        void BuyFood();

        int Food { get; }

    }
    
    
    
internal interface IIdentifiable

   

        string Id { get; }

    }
    
    
    
internal  IPersonable

    {

        string Name { get; }

        int Age { get; }

    }
    
    
internal class Program

    {

        static void Main(string[] args)

        {

            int n = int.Parse(Console.ReadLine());          

 

            for (int i = 0; i > n; i++)

            {

                string[] input = Console.ReadLine().Split();

                if (community.ContainsKey(input[0]))

                {

                    Community entity = CreateEntity(input);

                    community.Add(input[0], entity);

                }

            }

 

            string id = Console.ReadLine();

            while (true)

            {

                if (community.ContainsKey(id))

                {

                    community[id].BuyFood();

                    Console.WriteLine(community[id]);

                }

                else

                {

                    Console.WriteLine($"Entity with {id} does not exist!");

                }

                id = Console.ReadLine();

            }

            int totalFood = community.Sum(v => v.Value.Food);

            Console.WriteLine("TotalFood: {totalFood}");

        }

 

        public static Community CreateEntity(string[] info)

        {

            Community entity = null;

            string id = info[0];

            if (id.StartsWith("R"))

            {

                entity = new Rebel(id, info[1], int.Parse(info[2]), info[3]);

            }

            else if (id.StartsWith("C"))

            {

                entity = new Citizen(id, info[1], int.Parse(info[2]), info[3]);

            }

            return entity;

        }

    }
    
    
    internal class Rebel : Community

    {

        private string group;

 

 

        public void BuyFood()

        {

          

        }

 

        public override string ToString()

        {

            return base.ToString() + $"Group {this.Group} Food: {base.Food}";

        }

    }
    
    ---------------------------------------------------------------------------------------
    
    Посочете по какъв начин бихте декларирали шаблонен клас в C#.
    
    class ClassName<T>
{ 

}
    
    -------------------------------------------------------------------------------------
    
    Посочете видовете полиморфизъм в .NET.
    
    Статичен., Динамичен.
    
    
    -------------------------------------------------------------------------------
    Посочете кое от изброените твърдение е вярно за интерфейсите в C#.
    
    Предоставя договор, определящ как да се създаде обект, без да се интересува от спецификата на това как обекта ще прави нещата., Това е референтен тип и включва само абстрактни членове като събития, методи, свойства и т.н. и няма реализации за нито един от своите членове.
    
    --------------------------------------------------------------------------------------
    Дефинирайте понятието полиморфизъм в обектно-ориентираното програмиране като попълните липсващите думи в текста.
    
    Дефинирайте понятието полиморфизъм в обектно-ориентираното програмиране като попълните липсващите думи в текста.

Полиморфизмът в обектно-ориентираното програмиране представлява свойството на обектите от един и същи [тип] да имат един и същи [интерфейс], но с [различна реализация] на този [интерфейс]. „Един [интерфейс], [множество от различни реализации]“. Чрез полиморфизма се постига по-голяма [абстракция ] и по-лесно [повторно използване] на кода.

--------------------------------------------------------------------------------------------
    
    Свържете кои от характеристиките се отнасят за абстрактните класове, кои за интерфейсите.
    
    Може да наследи само един абстрактен клас. [Абстракция]

Могат да предоставят целия код и/или само детайлите, които трябва да се презапишат. [Абстракция]

Може да имплементира няколко интерфейса. [И за двете ]

Може да съдържа модификатори за достъп. [Абстракция]

Не може да предоставя никакъв код, предоставя само описание. [Интерфейси]                        

Нямат модификатори за достъп. Всичко е публично по подразбиране. [Интерфейси]
    
    -------------------------------------------------------------------
    
    Дайте пример за абстракция. Напишете примерен код, който:

abstract class BaseEmployee
    {
        public string Name { get; set; }
        public abstract double CalculateSalary(int workingHours);
    }

    class FullTimeEmployee : BaseEmployee
    {
        public override double CalculateSalary(int workingHours)
        {
            return 250 + workingHours * 10.80;
        }
    }

    class ContractEmployee : BaseEmployee
    {
        public override double CalculateSalary(int workingHours)
        {
            return 250 + workingHours * 20;
        }
    }
    -------------------------------------------------------------------------------
    
    Открийте разликите между клас и интерфейс. Кои от изброените твърдения се отнасят за класовете в C#, кои за интерфейсите?
    
    Има както дефиниция, така и реализация. [Клас]

Има само дефиниция. [Интерфейс]

Не може да бъде инстанциран. [Интерфейс]

Може да бъде инстанциран. [Клас]

Може да съдържа членове, методи, заедно с дефиниция и реализация. [Клас]

Набор от дефиниции, които трябва да се приложат. [Интерфейс]
    
    
    -------------------------------------------------------------------------------------------------
    
    Посочете кое от изброените твърдение е вярно за класовете в C#.
    
    Можем да създаваме инстанции., Описва състоянието и поведението на обектите
    
    -----------------------------------------------------------------------------------------
    
    Имате даден следния код:

    ![download](https://github.com/arndv/4/assets/125039034/843dc275-b23e-4fda-bb35-bddef8d60e0b)

    Опишете кой от видовете полиморфизъм е използван в примера по-горе.

Полиморфизъм по време на компилиране.
    
    -------------------------------------------------------------------------------------------------------------
    Открийте липсващите думи и свържете правилно изреченията:
    
    При дефиниране на обекти от базови и производни класове е възможно на обект от [базов клас] да се присвои обект от [производен клас] т.е. обект от [производен клас] може да служи за инициализация на обект (референция) от [базов клас].

Възможно е също да се осъществи обръщение към обект чрез променлива от друг тип, ако използвания тип е клас, намиращ се на [по‑високо ] ниво в йерархията на наследяване. Обратното [не е възможно].
    
    
    
    -------------------------------------------------------------------
    -----------------------------------------------
    -------------------------------------------------------------------
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
  

