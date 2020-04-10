## Compose and Pipe
- basic example
```JS 
const compose = (f, g) => data => f(g(data));
const pipe = (f, g) => data => g(f(data));

const multiplyBy3 = num => num*3;
const makePositive = num => Math.abs(num);

const multiplyBy3AndAbsolute = compose(
	multiplyBy3, 
	makePositive
);
multiplyBy3AndAbsolute(-150);
```

## Example
- a functional programming paradigm shopping cart
```JS
const user = {
	name: 'Kim',
	active: true,
	cart: [],
	purchases: []
}

const history = [];

const compose = (f, g) => (...args) => f(g(...args));
const pipe = (f, g) => (...args) => g(f(...args));

const purchaseItem = (...fns) => fns.reduce(compose);
const purchasesItem2 = (...fns) => fns.reduce(pipe);

purchasesItem2(
	addItemToCart,
	applyTaxToItems,
	buyItem,
	emptyUserCard
)(user, {name: 'laptop', price: 60});

function addItemToCart(user, item) {
	history.push(user);
	const updatedCart = user.cart.concat(item);
	return Object.assign({}, user, { cart: updatedCart });
};

function applyTaxToItems(user) {
	history.push(user);
	const { cart } = user;
	const taxRate = 1.3;
	const updatedCart = cart.map(item => ({
		name: item.name,
		price: item.price*taxRate
	}));
	return Object.assign({}, user, { cart: updatedCart });
};

function buyItem(user) {
	history.push(user);
	const itemsInCart = user.cart;
	return Object.assign({}, user, { purchases: itemsInCart });
};

function emptyUserCart(user) {
	history.push(user);
	return Object.assign({}, user, { cart: [] });
};
```











