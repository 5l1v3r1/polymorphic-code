polymorphic_code
================

The code should be encrypted and stored inside a string. The file, when running will decrypt the string and using eval will put the code into memory, accessible by the program

 
 
 if you want to add you own code: 
 
 1 - write your ruby code. 
 
 2 - Copy the gn(code) function into a new file
 
 3 - copy your code and send it by parameter to gn
 
 4 - Print the output of gn
 
 5 - Put the output of gn into the variable code

The code should be encrypted and stored inside a string. The file, when running will decrypt the string and using eval will put the code into memory, accessible by the program

if you want to add you own code: 
1 - write your ruby code. 
2 - Copy the gn(code) function into a new file
3 - copy your code and send it by parameter to gn
4 - Print the output of gn
5 - Put the output of gn into the variable code



      
      ******************
      *** generator ****
      ******************
      
      This function will generate an encrypted string given
      The scring given should be code for the application
      
      the best way to explain this is by explaining the encryption algorithym
      
      Lets suppose we want to encrypt the letter a
      first we convert it into ascii 
       >> a = 97
      next will generate a random number beetween 1 and 100 and call it y
       >> lets say y = 10
      now need to generate the k to know the operation to be used... k can be 2,3 or 4
       >> lets say y = 3
      
      so to encrypt a will be using the operation 3 that is a multiplication
      so we will multiply a with y
       >> 97 * 3
      
      our encrypted a will be 291
      
      To decrypt 291 we need to do the inverse of this. So we know y and k...
      a = 291 / 3
      We know that we need to divide 291 cause k is 3 which means an multiplication was used, so the inverse of it is the division
      
      def gn(code)
      
       
       final = ""
       
       code.each_char do |c|  
         k = Random.rand(2...4)
         y = Random.rand(1...100)
         
         if k==2
           asc = c.ord - y
         elsif k==3
           asc = c.ord*y
         elsif k == 4
           asc = c.ord + y
         end
         
         final << "rd(#{asc},#{y},#{k}) + "
         
       end
       
       return final[0...-3]
       
      end
        
      gen is the generator that will encrypt the code.
      code is the encrypted code to be ran
      b and s are internal code needed by the application
      
      
        
      ******************
      *** code  in b ***
      ******************
      
      function to override the existing file with a new encrypted code
      def mt(f,s,b, gen, code)
       
       t = ""
       i = 0
       File.readlines(f).each do |line|
         t << line
         i = i + 1
         break if i == 15
       end
       
       t << "\n"
       t << b
       t << "\n#{gen}"
       t << "\n#{code}\n"
       t << "s = \"#{s}\"\n"
       t << "eval eval b\n"
       t << "eval s\n"
       t << "mt(__FILE__,s,b,gen,code)\n"
      
       File.open(f, "w") { |file| file.write(t)} 
      end
      
      decrypt and put into memory generator code
      def ds_g(gen)
       g = eval(gen)
       eval(g)
       g1 = "gen = \"#{gn(g)}\""
      end
      
      
      def ds_c(code)
       pl = eval code
       eval pl
       pl1 = "code = \"#{gn(pl)}\""
       
      end
      
      decrypt and put into memory generator code
      def ds_b(b)
       v = eval(b)
       eval v
       v1 = "b = \"#{gn(v)}\""
      end
