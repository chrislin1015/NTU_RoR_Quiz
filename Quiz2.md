1. 請用簡單的方式敘述以下每一行程式碼：
   ```ruby
   a = 1 
   @a = 2
   @@a = 5
   user = User.new
   user.name
   user.name = "Joe"
   ```
   * 宣告一個變數a並且指派數值1到變數a
   * 宣告一個實例變數a並且指派數值2到實例變數a
   * 宣告一個類別變數a並且指派數值5到類別變數a
   * 建立一個User類別實例並指派給變數user
   * 取得user物件的實例變數name
   * 指派"Joe"字串給user物件的實例變數name
  
2. 什麼是 module? 請寫一段程式碼說明一個 class 要如何使用一個 module 裡面的 method?
   
   module是將相關的方法與常數包在一起，提供特定的功能讓需要的人使用。就像是一個工具箱一樣。
    
   module的限制有
      * 不可以new，無法被實例化
      * 不能被繼承
   
   module的功用有
      * 定義一些公用的函式庫，提供他人使用，例如Ruby裡的Math模組
      * 讓其他類別透過mixin方式引用，擴充功能
   ```ruby
   module Fly
     def fly
       puts "I can believe I can fly!"
     end
   end
   class People
     include Fly
     def initialize
     end
     def walk
       puts "keep walking!"
     end
   end
   people = People.new
   people.fly
   ```

3. 請說明 class variable 和 instance variable 之間的差別

    |      |宣告方式|使用方式| 
    |------|:-------:|:--------:|
    |class variable| @@name，變數名稱前加上@@，並且在類別的最外層宣告|使用時直接透過類別名稱.變數名稱就可以使用|
    |instance variable|@name，變數名稱前加上@，並且只能宣告在函式裡，通常是宣告在initialize|必須先建立好實例，才可以透過實例物件來進行存取|   
   ```ruby
   class Mario
     attr_accessor :life, :star
     @@pass_level = 1
     def initialize
       @life = 5
       @star = 0
     end
   end
   mario = Mario.new
   puts Mario.pass_level  # 存取類別變數
   puts mario.life        # 存取實例變數
   ```

4. 請說明 class method 和 instance method 之間的差別

    |      |宣告方式|使用方式| 
    |------|:-------:|:--------:|
    |class method|在method名稱前加上self.|使用時直接透過類別名稱.method名稱就可以使用|
    |instance method|一般method的宣告方式|必須先建立好實例，才可以透過實例物件來進行存取|   
   ```ruby
   class Mario
     def initialize
     end
     def self.hello
       puts "It's me, Mario!"
     end
     def start
       puts "Here we go!!!"
     end
   end
   mario = Mario.new
   puts Mario.hello  # 存取class method
   puts mario.start  # 存取instance method
   ```

5. 如果今天我為一個叫 User 的 class 產生一個新物件的方式是:
   ```ruby
   User.new("Bob", "male", "Engineer")
   ```
   請寫出 User class 的 initialize method
   ```ruby
   class User
     def initialize(name, sex, job)
       @name = name
       @sex = sex
       @job = job
     end
   end
   ```

6. 在： A.  一個 class 裡，method 外面 B.  一個 class 裡，instance method 裡，self 分別是指向什麼?
  
   在定義一個class時，將self放在method外面就等同於是在類別層級的宣告，此時的Self是指向class。在method裡宣告的self是物件層級，指向的是呼叫該method的物件。

7. attr_accessor 的功能是什麼，它和 attr_reader、attr_writer 之間的差別是什麼？

   attr_accessor會幫你在Ruby的類別裡產生一對getter以及setter方法。attr_reader則只會產生getter，相對的attr_writer只會產生Setter。
   在Ruby的類別裡宣告的實例變數，為了保持資訊隱藏的特性，Ruby的變數預設都是被保護的，也就是外部無法直接存取。如果真的要取得或是設定，則必須寫對應的函式才能達到效果。
   ```ruby
   class Player
     def initialize
       @name = "Chris"
     end
     def getName
       return @name
     end
     def setName(value)
       @name = value
     end
   end
   ```
    但是如果每個實例變數都要加上對應的存取函式，將會造成些許的不方便。所以只要加上attr_accessor、attr_reader、attr_writer這些指令就可以直接存取。

8. 請說明 public 和 private method 之間的不同

   ruby的method存取權限分為三種
   * public：在任何地方都可以存取，如果沒有特別標示，預設就是public
   * protected：只有在同一個類別內、同一個package或是繼承的子類別可以存取
   * private：除了類別內部可以存取之外，一律不可以被存取
   ```ruby
   class ThisIsClass
     def method_a
       puts "This is public method"
     end
     protected
     def method_b
       puts "This is protected method"
     end
     private
     def method_c
       puts "This is private method"
     end
   end
   ```

9. 請說明 Inheritance 和 Module 之間的差別，它們分別是用於哪些情況？ 請舉例說明

   類別可以透過繼承或引用模組的方式來擴充功能達到程式碼再利用的特性。Inheritance是一種"Is a"的概念，而Module是一種"has a"的概念。透過繼承你可以很快的擴充並沿用父類別有的變數與方法，但是由於繼承是一個榜定與緊耦合的關係。
    讓我們來看一個案例，今天有一個飲料店有一系列的茶飲。茶飲類別最基本的就是一個class Tea。裡面提供了甜度、溫度的設定。首先販賣紅茶與綠茶，個別繼承了Tea，宣告為class BlackTea < Tea，class GreenTea < Tea。後來業績長紅，決定擴充產品，推出奶茶與奶綠。繼承於BlackTea與GreenTea。宣告為class MilkTea < BlackTea，class GreenMilkTea < GreenTea。
    雖然生意變好了，不過痛苦的要開始了。有客人開始要求不要用奶精要用鮮奶。只好再擴充class BlackTeaWithMilk < BlackTea，class GreenTeaWithMilk。光是奶類就擴充了四個類別，已經開始恐怖了起來。再加上珍珠奶茶開始流行，又必須加上珍珠這個配料，如果每個飲品都要加，那真的才是惡夢。而這就是所謂的類別爆炸。
    透過繼承雖然可以很快的擴充功能，但是由於耦合度過高，無法很有彈性地去擴充。有很多相似的功能卻要被重複撰寫幾次。如果透過module，將各種相同的功能抽離出來，定義為一個一個module，在需要的類別裡去引用，來達到擴充與再利用。以剛剛的案例，我們就可以將奶精、鮮奶、珍珠等配料個別獨立為一個module。module Creamer、module Milk、module Pearl。提供給Tea引用
   ```ruby
   class Tea
     include Creamer
     include Milk
     include Pearl
   end
   ```
    只要在各個module提供使用量的方法，讓後續繼承的class能夠根據需求設定。如果不需要奶精就設為0，如此，後續衍伸的產品都可以獨立增加各種配料而不需要因為配料的增加而擴充類別。
    
10. 若今天有一個 class 有 include 一個 module，他的 parent class 和 sub class 是否可以使用該 module 裡的 method?

    parent class無法使用module裡的method，sub class則可以使用

11. 請間單說明什麼是 Relational Database，什麼是 SQL

    關聯式資料庫是採用關係模型作為數據組織方式，再依此基礎建出系統架構的資料庫。關聯式資料庫的特點在於它將每個具有相同屬性的數據獨立地存儲在一個表中。對任一表而言，用戶可以新增、刪除和修改表中的數據，而不會影響表中的其他數據
    
    SQL，結構化查詢語言（Structural Query Language），是一種特殊目的之程式語言，用於資料庫中的標準資料查詢語言，作為關係式資料庫管理系統的標準語言
