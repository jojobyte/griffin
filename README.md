# griffin

A peer-to-peer document-oriented database. Take back ownership over your data!

Griffin is a decentralized database powered by [GUN](https://github.com/amark/gun) that implements an API and query language similar to MongoDB. All data stored is automatically encrypted and distributed over a peer-to-peer network and can optionally be shared with others. It is a truly powerful database solution.

## Usage

`yarn add griffin-browser` or `yarn add griffin-nodejs`

```js
import Griffin from "griffin-browser"

const griffin = Griffin()
await griffin.auth("username", "password")

const db = griffin.namespace("my-app")
const app_specific_key = await db.gen() // This is an optional 12 word mnemonic generated by the user
await db.auth(app_specific_key)

const dogs = await db.collection("dogs")

await dogs.insert([
	{ name: "Gordon", color: "black", age: 3, owners: ["John", "Cindy"] },
	{ name: "Pooch", color: "brown", age: 5, owners: ["John", "Cindy"] },
	{ name: "Snuffles", color: "brown", age: 7, owners: ["Karen"] },
	...
]).many()

console.log(await dogs.find({ color: "brown" }).sort({ name: 1 }).one())
console.log(await dogs.find({ name: { $or: ["Gordon", "Pooch"] } }).fields({ _id: 0 }).many())
console.log(await dogs.find({ age: { $lt: 7, $gte: 3 } }).limit(10).many())

await dogs.update({ age: 5 }, { $inc: { age: 1 } }).one()
await dogs.replace({ name: "Gordon" }, { name: "Gordon Ramsey", color: "blonde", age: 54, owners: null })
```

## Donations

Feel free to donate! I plan on implementing the entire MongoDB API, a file storage API based on Sia/Skynet and other features involving shared data.

I can work on this much more frequently with a more sustainable income. All donations will go to living expenses, assets, servers and Sia file storage costs (I plan on running my own Skynet portal).

Liberapay: https://liberapay.com/giraffekey/
