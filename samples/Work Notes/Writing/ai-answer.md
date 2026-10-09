---
source: AI assistant answer, saved as Markdown
question: "How do I plan a week of dinners on a budget?"
saved: 2026-10-06
---

# How to plan a week of dinners on a budget

> [!NOTE]
> An AI assistant's answer, saved as a `.md` file. Prices are examples, not today's prices
> in your shop.

Short answer: plan around **two or three cheap staples**, cook in **batches**, and let
**leftovers** cover two or three nights. For one person, the shopping comes to about
**€22**, and the dinners in this plan use **€9.50** of it – the rest lasts into next week.

## A sample week

| Day | Dinner | Uses leftovers from | Cost (€) |
|:--|:--|:--:|--:|
| Mon | Lentil and carrot soup | – | 1.40 |
| Tue | Baked potatoes with eggs | – | 1.30 |
| Wed | Soup and toast | Mon | 0.90 |
| Thu | Chicken thighs with rice and peas | – | 2.60 |
| Fri | Fried rice with egg | Thu | 1.20 |
| Sat | Tomato pasta | – | 1.10 |
| Sun | Potato and onion tray bake | Tue | 1.00 |
| | **Week** | | **9.50** |

> [!TIP]
> The weekly cost per dinner is lower than the shop total, because staples like rice, pasta
> and lentils last more than one week.

## The method

1. **Check what you already have.** Fridge, freezer, cupboards – plan two meals around
   whatever needs using up.
2. **Pick two cheap proteins.** Dried lentils, beans, eggs and chicken thighs cost less per
   portion than most alternatives.
3. **Cook once, eat twice.**
   - Make a double batch of soup or sauce.
   - Freeze half in single portions.
4. **Write the list by recipe, not by shelf.** Every item should belong to a named meal.
5. **Buy loose and in season.** Loose vegetables are usually cheaper than packed ones.

## Cost per portion

Divide the price by the number of portions:

$$
\text{cost per portion} = \frac{\text{price of the pack}}{\text{portions in the pack}}
$$

For example, a 1 kg bag of lentils at €2.40 gives about 12 portions, so
$\frac{2.40}{12} = 0.20$, or €0.20 per portion.

| Staple | Pack | Price (€) | Portions | Per portion (€) |
|:--|:--|--:|--:|--:|
| Dried lentils | 1 kg | 2.40 | 12 | 0.20 |
| Rice | 1 kg | 1.90 | 12 | 0.16 |
| Pasta | 1 kg | 1.30 | 10 | 0.13 |
| Eggs | 12 | 3.00 | 6 | 0.50 |
| Chicken thighs | 1 kg | 5.50 | 5 | 1.10 |

## Shopping list

- [ ] Dried lentils, 1 kg
- [ ] Rice, 1 kg
- [ ] Pasta, 1 kg
- [ ] Chicken thighs, 1 kg
- [ ] Eggs, 12
- [ ] Potatoes, 2.5 kg
- [ ] Carrots and onions, 1 kg each
- [ ] Tinned tomatoes, 4 tins
- [ ] Frozen peas

## Check your total before you shop

A few lines of Python add up the list:

```python
basket = {
    "lentils 1 kg": 2.40,
    "rice 1 kg": 1.90,
    "pasta 1 kg": 1.30,
    "chicken thighs 1 kg": 5.50,
    "eggs x12": 3.00,
    "potatoes 2.5 kg": 2.00,
    "carrots 1 kg": 0.90,
    "onions 1 kg": 1.10,
    "tinned tomatoes x4": 2.20,
    "frozen peas": 1.50,
}

total = sum(basket.values())
print(f"Shop total: €{total:.2f}")   # €21.80
```

<details>
<summary>Recipe: lentil and carrot soup (4 portions)</summary>

1. Fry one chopped onion and two chopped carrots in a little oil for 5 minutes.
2. Add 200 g dried lentils and 1 litre of stock.
3. Simmer for 25 minutes, until the lentils are soft.
4. Season, then blend half of it for a thicker soup.

Two portions for Monday, one for Wednesday, one for the freezer.

</details>

> [!WARNING]
> Cool cooked rice quickly and keep it in the fridge. Eat it within a day.[^rice]

If your total is above your limit, swap the chicken night for a bean dish and add it up again.

[^rice]: This is the usual food-safety advice for cooked rice.
