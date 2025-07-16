# ex-js-objects-snack-2
EX - Snack Oggetti
Repo: ex-js-objects-snack-2
🏆 Code Question 1
const hamburger = { name: "Cheese Burger", weight: 250 };
const secondBurger = hamburger;
secondBurger.name = 'Double Cheese Burger';
secondBurger.weight = 500;
​
console.log(hamburger.name); // ?
console.log(secondBurger.name ); // ?
Senza lanciare il codice, riesci a prevedere cosa viene stampato in console?
Quanti oggetti sono stati creati in memoria durante l'esecuzione di questo codice?

SOLUZIONE:

1. console.log(hamburger.name);  { name: "Double Cheese Burger", weight: 500 };
console.log(secondBurger.name );  { name: "Double Cheese Burger", weight: 500 };
Verrà stampato in console lo stesso oggetto, le modifiche apportate con secondBurger.name e secondBurger.weight sono visibili sia per hamburger che per secondBurger, in quanto la copia di secondBurger su hamburger è avvenuta per Reference type (non si crea un nuovo oggetto, ma un riferimento allo stesso oggetto, creato in memoria inizialmente da hamburger)

2. E' stato creato in memoria un solo oggetto, nel momento in cui ho inizializzato e dichiarato hamburger vado a creare in memoria il suddetto oggetto con il suo riferimento a hamburger, nel momento in cui vado a effettuare una reference copy di hamburger su secondBurger, sto salvando in secondBurger un nuovo riferimento allo stesso oggetto in memoria 

----------------------------------------------------------------------------------------------------------

🏆 Code Question 2
const hamburger = { 
    name: "Cheese Burger", 
    weight: 250,
    ingredients: ["Cheese", "Meat", "Bread", "Tomato"]
};
​
const secondBurger = {...hamburger};
secondBurger.ingredients[0] = "Salad";
​
console.log(hamburger.ingredients[0]); // ?
console.log(secondBurger.ingredients[0]); // ?
P.S.: Ricordati che gli Array, come gli oggetti, sono dei Reference Type (Tipi di Riferimento)!
Senza lanciare il codice, riesci a prevedere cosa viene stampato in console?
Quanti oggetti sono stati creati in memoria durante l'esecuzione di questo codice?

SOLUZIONE:

1. console.log(hamburger.ingredients[0]);
 
 "Salad"

console.log(secondBurger.ingredients[0]); 
 
 "Salad"

In questo modo avviene una shallow copy ossia una copia superficiale, copia tutto l'ggetto hamburger ma per i suoi oggetti annidati fa una copia per riferimento (reference copy)
In questa maniera, se andiamo a modificare un ingrediente (che è una proprietà annidata dell'oggetto hamburger) verrà modificata sia in hamburger che in secondBurger in quando la copira di ingredients è avvenuta per riferimento ( potevamo ovviare a questo problema scrivendo così const secondBurger = {...hamburger, ingredients: {...hamburger.ingredients}}; in questa maniera hamburger è un nuovo oggetto che avrà a sua volta come proprietà un nuovo oggetto per ingredients )

2. Sono stati creati due oggetti in memoria usando il metodo shallow copy con lo spread operator (copia di primo livello), i due oggetti avranno all'interno la propietà ingredients che è un oggetto annidato, questa proprietà è stata copiata per riferimento ossia non è stata creata una nuova copia per questa, qualsiasi modifica toccherà entrambi gli oggetti (hamburger e secondBurger)

----------------------------------------------------------------------------------------------------------
🏆 Code Question 3
const hamburger = { 
    name: "Cheese Burger", 
    weight: 250,
    maker: {
        name: "Anonymous Chef",
        restaurant: {
            name: "Hyur's Burgers",
            address: "Main Street, 123",
            isOpen: true,
        },
        age: 29
    }
};
​
const secondBurger = structuredClone(hamburger);
const thirdBurger = structuredClone(hamburger);
Quanti oggetti sono stati creati in memoria durante l'esecuzione di questo codice?

SOLUZIONE

1. Abbiamo trè oggetti in memoria:

-hamburger

-secondBurgher (creato col metodo structuredClone() che effettua una copia profonda sull'oggetto copiato, copiando anche gli oggetti annidati e complessi, crea un clone strutturato )

-thirtBurger (creato col metodo structuredClone() che effettua una copia profonda sull'oggetto copiato, copiando anche gli oggetti annidati e complessi, crea un clone strutturato )

----------------------------------------------------------------------------------------------------------

🏆 Code Question 4
const chef = {
    name: "Chef Hyur",
    age: 29,
    makeBurger: (num = 1) => {
        console.log(`Ecco ${num} hamburger per te!`);
    },
}
​
const restaurant = {
    name: "Hyur's Burgers",
    address: {
        street: 'Main Street',
        number: 123,
    },
    openingDate: new Date(2025, 3, 11),
    isOpen: false,
};
Qual è il metodo migliore per clonare l’oggetto chef, e perché?
Qual è il metodo migliore per clonare l’oggetto restaurant, e perché?
🎯 Code Question 5 (Bonus)
const hamburger = { 
    name: "Cheese Burger", 
    weight: 250,
    maker: {
        name: "Anonymous Chef",
        restaurant: {
            name: "Hyur's Burgers",
            address: "Main Street, 123",
            isOpen: true,
        },
        age: 29
    }
};
​
const newRestaurant = {...hamburger.maker.restaurant};
newRestaurant.name = "Hyur's II";
newRestaurant.address = "Second Street, 12";
const secondBurger = {...hamburger};
secondBurger.maker.restaurant = newRestaurant;
secondBurger.maker.name = "Chef Hyur";
​
console.log(hamburger.maker.name); // ?
console.log(secondBurger.maker.name); // ?
console.log(hamburger.maker.restaurant.name); // ?
console.log(secondBurger.maker.restaurant.name); // ?
Senza lanciare il codice, riesci a prevedere cosa viene stampato in console?
Quanti oggetti sono stati creati in memoria durante l'esecuzione di questo codice?
🎯 Code Question 6 (Bonus)
const chef = {
    name: "Chef Hyur",
    age: 29,
    makeBurger: (num = 1) => {
        console.log(`Ecco ${num} hamburger per te!`);
    },
    restaurant: {
        name: "Hyur's Burgers",
        welcomeClient: () => {
            console.log("Benvenuto!");
        },
        address: {
            street: 'Main Street',
            number: 123,
            showAddress: () => {
                console.log("Main Street 123");
            }
        },
        isOpen: true,
    }
}
Qual è il metodo migliore per clonare l’oggetto chef, e perché?
🎯 Snack  (Bonus)
Crea una funzione che permette la copia profonda (deep copy) di un oggetto, che copia anche i suoi metodi (proprietà che contengono funzioni). Usa l’oggetto di Code Question 6 come test.

⚠️ Serve usare una funzione ricorsiva! (fai un po’ di ricerca).
