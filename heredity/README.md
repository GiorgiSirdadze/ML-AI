# Heredity Probability Functions

So, for this heredity task, I had to write a few functions to calculate probabilities related to genes and traits within a family. Here's how I approached it:

## 1. `check_copies_helper(person, one_gene, two_genes)`

* **What it does:** This one's pretty simple. It just figures out how many copies of a gene a person has (0, 1, or 2).
* **How I did it:**
    * I check if the person is in the `one_gene` set (meaning they have one copy).
    * If not, I check if they're in the `two_genes` set (two copies).
    * If they're in neither, they have zero copies.

## 2. `probs_no_parents(copies_gene, has_trait)`

* **What it does:** This calculates the probability of someone having a specific number of gene copies *and* a trait if they don't have parents listed in the data.
* **How I did it:**
    * I just multiply the unconditional probability of having that gene count (`PROBS["gene"][copies_gene]`) by the probability of having the trait given that gene count (`PROBS["trait"][copies_gene][has_trait]`).

## 3. `probs_has_parents(person, people, one_gene, two_genes, have_trait)`

* **What it does:** This is the big one! It calculates the probability of a person's gene count and trait when we *do* know their parents.
* **How I did it:**
    * I get the parents' gene counts using `check_copies_helper`.
    * I calculate the probability of each parent passing on a gene (50% chance each).
    * I factor in the mutation rate (`PROBS["mutation"]`) to get the probabilities of passing on a gene with or without a mutation.
    * Then, I calculate the probability of the child having the correct gene count based on all the possible parent gene combinations.
    * Finally, I multiply that gene probability by the probability of having the trait given the gene count.

## 4. `joint_probability(people, one_gene, two_genes, have_trait)`

* **What it does:** This calculates the overall probability of *everyone* in the family having the specified gene counts and traits.
* **How I did it:**
    * I loop through each person in the `people` dictionary.
    * I use `probs_no_parents` or `probs_has_parents` (depending on whether the person has parents) to get their individual probability.
    * I multiply all these individual probabilities together to get the joint probability.

## 5. `update(probabilities, one_gene, two_genes, have_trait, p)`

* **What it does:** This adds a joint probability `p` to the running totals in the `probabilities` dictionary.
* **How I did it:**
    * I loop through each person.
    * I get their gene count using `check_copies_helper`.
    * I add the probability `p` to the appropriate gene and trait values in the `probabilities` dictionary.

## 6. `normalize(probabilities)`

* **What it does:** This makes sure the probabilities for each person's gene counts and traits add up to 1.
* **How I did it:**
    * I loop through each person.
    * I sum up all the gene probabilities and all the trait probabilities.
    * I divide each individual gene and trait probability by their respective sums to normalize them.

## Honestly...

* This was a bit tricky to get my head around, especially the `probs_has_parents` function.
* I tried to break it down into smaller, more manageable steps.
* I think the code is pretty clear, but I'm still learning about genetic probabilities.
* Let me know if you have any questions!
