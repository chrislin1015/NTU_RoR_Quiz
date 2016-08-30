1. 請說明 Fixnum (整數) 和 Float (浮點數) 之間的差異
> Fixnum是表示0,1,2等整數，可以有正負值
> Float是表示0.1,0.5,3.14等有小數的數值，同樣也有正負值
> Fixnum與Fixnum的運算結果都會是Fixnum，Float與Float的運算也是Float．但是Fixnum與Float的運算結果會是以Float表示

2. 今天有兩個字串：
  ```ruby
  str1 = "Hallo Welt!" 
  str2 = " NTU Rails 261!"
  ```
請說明以下兩個印出字串的方式的不同處：
  ```ruby
  puts str1 + str2
  puts "#{str1}#{str2}"
  ```
> 輸出的結果是一樣的，不過第一行的字串相加，是字串間經過＋這個operator，會經過函式的堆疊與記憶體的搬移．第二行是直接經過字串將變數轉換的方式，直接輸出成一個字串，是直接透過編譯器轉換．

3. 請解釋 array 和 hash 的不同處
> array與hash都是一種資料結構，目的是將資料收集起來，方便日後存取。兩個的不同點是
> array
> 將物件有序的集合起來，並用數值索引的方式來存取物件。陣列的內容可以是任意物件，包括整數、浮點數、字串、物件、陣列、Hash。
  
  ```ruby
  arr = [1, "Chirs",  0.3]
  #陣列的索引必須是整數，以0為起始
  puts arr[0]  #印出1
  puts arr[1]  #印出Chris
  ```
  
> hash
> 將物件透過鍵(key)值(value)對的方式成對表示，透過Key來存取對應的value。key可以是字串、整數、symbol也可以是物件

  ```ruby
  man = {
            name: "Chris",
            age: 37,
            occupation: "Programmer"
          }
  # 只能透過key來存取
  puts man[:name]  # 印出Chris
  ```

4. 請用一行程式碼從 [1, "a string", 3.14, [1,2,3,4]] 這個陣列找出所有非字串的值
  ```ruby
  arr.select { |x| x.is_a? string }
  ```

5. 請用一行程式碼把一個內容為整數 1 到 100 的陣列裡所有的值加上 2
  ```ruby
  arr.map! { |x| x += 2 }
  ```

6. 請寫出以下兩行程式碼迴傳的值，並解釋他們呼叫的方法差別為何：
  ```ruby
  [1, 2, 3, 3].uniq
  [1, 2, 3, 3].uniq!
  ```
> uniq是將陣列裡重複的項目移除，回傳出獨一無二的陣列資料。uniq是將處理過的結果輸出一個新的陣列，並不會改變本來陣列的內容。uniq!與uniq得到的陣列是一樣的，唯一不同的是uniq!是直接修改原本的陣列，並不會額外儲存在新的陣列裡

  ```ruby
  arr = [1, 2, 3, 3]
  puts arr.uniq  #=> [1, 2, 3]
  puts arr       #=> [1, 2, 3, 3] 並沒有改變
  puts arr.uniq! #=> [1, 2, 3]
  puts arr       #=> [1, 2, 3] 已經改變了
  ```

7. 請列出兩種產出亂數的方法
  ```ruby
  # 用array的sample，會隨機取樣一個陣列內容出來
  arr = [1, 2 , 3]
  puts arr.sample
  # 用array的shuffle!
  puts arr.shuffle!.first
  # 用Random類別
  var = Random.rand(1..3)   # 1~3隨機一個數
  var = Random.rand(1...3)  # 1~2隨機一個數，不包含3
  ```

8. 以下這段程式碼：
  ```ruby
  ((1 > 3)&&(true == true))||(!!!false)
  ```
會執行出什麼結果？ 請試試不用 irb 算出結果
> 回傳True

9. 請問 binding.pry 是什麼？ 要如何使用它？
> binding.pry是Ruby在執行時期中斷程式的方法。要能夠進行中斷除錯，必須先安裝pry這個套件
> 安裝方法
  ```
  $ gem install pry
  $ gem list pry
  $ gem uninstall pry-nav 
  ```
> 使用方法
  ```ruby
  # 首先在需要進行中斷的ruby程式碼檔案的最上面加上引用的語法
  reguire 'pry'
  var = "Hello World"
  # ˇ在要確認變數內容的下一行加上binding.pry
  binding.pry
  puts var
  ```

10. 下面的一段程式碼，請嘗試用其他方法把 if...else...end 簡化成一行
  ```ruby
  var = 5
  if var >= 5
        return "var is greater than or equal to 5"
  else
        return "var is less than 5"
  end
  ```
  ```ruby
  var = 5
  return var >= 5 ? "var is greater than or equal to 5" : "var is less than 5"
  ```

11. 請列出兩種不同的 hash 寫法
> 使用hashrocket寫法
  ```ruby
  person = { 
               :name => "Bob", 
               :age => 30,
               :occupation => "Engineer"
             }
  ```
  
> 但是松本大師認為很醜，改為這樣

  ```ruby
  person = { 
               name: "Bob",
               age: 30,
               occupation: "Engineer"
             }
  ```
