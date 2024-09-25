# checkpoint-OOP


// Classe Product pour stocker les propriétés d'un produit  
class Product {  
    constructor(id, name, price) {  
        this.id = id;  
        this.name = name;  
        this.price = price;  
    }  
}  

// Classe ShoppingCartItem pour stocker un produit et sa quantité  
class ShoppingCartItem {  
    constructor(product, quantity) {  
        this.product = product;  
        this.quantity = quantity;  
    }  

    // Méthode pour calculer le prix total de l'élément  
    getTotalPrice() {  
        return this.product.price * this.quantity;  
    }  
}  

// Classe ShoppingCart pour gérer le panier d'achat  
class ShoppingCart {  
    constructor() {  
        this.items = [];  
    }  

    // Méthode pour ajouter un élément au panier  
    addItem(product, quantity) {  
        const item = this.items.find(i => i.product.id === product.id);  
        if (item) {  
            // Si l'élément existe déjà, on augmente la quantité  
            item.quantity += quantity;  
        } else {  
            // Sinon, on ajoute un nouvel élément  
            const cartItem = new ShoppingCartItem(product, quantity);  
            this.items.push(cartItem);  
        }  
    }  

    // Méthode pour supprimer un élément du panier  
    removeItem(productId) {  
        this.items = this.items.filter(item => item.product.id !== productId);  
    }  

    // Méthode pour obtenir le total des éléments dans le panier  
    getTotalItems() {  
        return this.items.reduce((total, item) => total + item.quantity, 0);  
    }  

    // Méthode pour obtenir le montant total du panier  
    getTotalPrice() {  
        return this.items.reduce((total, item) => total + item.getTotalPrice(), 0);  
    }  

    // Méthode pour afficher les éléments du panier  
    displayItems() {  
        this.items.forEach(item => {  
            console.log(`${item.product.name} (x${item.quantity}): $${item.getTotalPrice().toFixed(2)}`);  
        });  
    }  
}  

// Exemple de test  
// Création de produits  
const product1 = new Product(1, "Apple", 0.5);  
const product2 = new Product(2, "Banana", 0.3);  
const product3 = new Product(3, "Orange", 0.8);  

// Création d'un panier d'achat  
const cart = new ShoppingCart();  

// Ajout d'éléments au panier  
cart.addItem(product1, 3); // 3 Apples  
cart.addItem(product2, 2); // 2 Bananas  
cart.addItem(product3, 4); // 4 Oranges  

// Afficher le panier  
console.log("Items in the cart:");  
cart.displayItems();  
console.log(`Total items in cart: ${cart.getTotalItems()}`);  
console.log(`Total price: $${cart.getTotalPrice().toFixed(2)}`);  

// Suppression d'un élément du panier  
cart.removeItem(2); // Remove Bananas  

// Afficher le panier après suppression  
console.log("\nItems in the cart after removal:");  
cart.displayItems();  
console.log(`Total items in cart: ${cart.getTotalItems()}`);  
console.log(`Total price: $${cart.getTotalPrice().toFixed(2)}`);
