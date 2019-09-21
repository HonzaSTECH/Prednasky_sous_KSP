# Jazyk Rust
### *Vašek Šraier a Standa Lukeš*
### *18.09.2019*

Podobné jazyku C - kompilovaný, nízkoúrovňový a rychlý

Koncepty z vyšších programovacích jazyků

Citlivý kompilátor - když se podaří program zkompilovat, obvykle funguje dobře, ale donutit ho se zkompilovat je často oříšek

Hello world program:

`
fn main(){
  println!("Hello world!");
  }
`

Definice proměnné:

`let x : i32 = 3;`

Tisk proměnné:

`println!("X je {}", x);`

Typy proměnných:
  - i8, i16, i32, i64
  - u8, u16, u32, u64, u128
  - bool
  - f32, f64
  - usize, isize

Inference typů - Rust sám rozhodne, jakého typu proměnná bude, pokud ji deklarujeme takto:

`let x = 3;`

Proměnné jsou neměnné, pokud není při jejich deklaraci použito `mut`

`
let mut x = 3;
x = x + 2; //Chyba
`

Proměnné se dají přepisovat - vytvoří se nová se stejným jménem a stará se zahodí

`
let x = 3;
let x = x + 2;
`

Definice funkce

`
fn abs(a: i32) -> i32 {
  if a > 0 {
    a
  } else {
    -a
  }
}
`

Expression block - navrací svou hodnotu (zde 0 nebo první prvek nějakého pole)

`
let neco = {
  let a = sezen_data();
  if (a.len() > 0){
    a[0]
  } else {
    0
  }
}
`

Nekonečný cyklus (stejné jako while(true){}):

`
loop {
  //Delej neco
}
`

Deklarace vlastních struktur:

`
struct User {
  name: String,
  fingers: Int
}
`

Implementace vlastních struktur:

`
impl User {
  fn new(name: String, fingers: u8) -> User {
    User {
      name,
      fingers: fingers
    }
  }
  fn cut_finger (&mut self){
    self.fingers -= 1;
  }
}
`

Používání vlastních struktur:

`
let mut u = User::new(String::from("Standa"), 20);
u.cut_finger();
`

Tuple = soubor hodnot

`
let a: (u8, &str, User) = (1, "Ahoj", u);
let x,y,z = a; //x = 1, y = "Ahoj", z = objekt User se jménem "Standa"
let (_,q,_) = a; //q = "Ahoj"
`

Enum = výpis možností, které u sebe mohou mít další informace

`
enum ReadResult {
  Success(i32),
  Error(String)
}
enum PaymentType {
  Cash,
  CreditCard(CardDetails),
  Transfer{ token: String }
}
`

Match

`
let result = neco_precti();
match result {
  Success(n) => println!("Success {}", n),
  Error(_) => {
    eprintln!("Je to rozbity!");
    panic!(); //Konec programu
  }
}
`

Ownership - každá proměnná má vlastníka

`
fn process(a: User){ ... }
fn main() {
  let a = User ::new(...);  //Dostaneme vlastnictví objektu
  let b = a;                //Přesuneme vlastnictví - a již nemůžeme použít
  process(b);               //Můžeme
  process(b);               //Nemůžeme
}
`

Reference
`
fn remove_name(a. &mut User) {
  a.name = String::from("UNDISCLOSED");
}
fn main() {
let u = User::new(...);
remove_name(&mut u);  //Zapůjčení mutable reference
u.name = "Pepík";     //Můžeme upravovat
}
`

Do VS Code lze přidat rozšíření rust-lang - vývojové prostředí

Dokumentace: **RustBook** (dostupná i na GitHub)