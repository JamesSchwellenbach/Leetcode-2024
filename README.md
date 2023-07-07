# Leetcode 2024. Maximize the Confusion of an Exam (Medium)

# Problem

A teacher is writing a test with n true/false questions, with 'T' denoting true and 'F' denoting false. He wants to confuse the students by maximizing the number of consecutive questions with the same answer (multiple trues or multiple falses in a row).

You are given a string answerKey, where answerKey[i] is the original answer to the ith question. In addition, you are given an integer k, the maximum number of times you may perform the following operation:

Change the answer key for any question to 'T' or 'F' (i.e., set answerKey[i] to 'T' or 'F').
Return the maximum number of consecutive 'T's or 'F's in the answer key after performing the operation at most k times.

Solution O(N)

Convert the answerKey string into a list that captures how many trues and falses in a row there are, negative numbers for falses positive numbers for trues. Then iterate through that list once, keeping track of a leftmost index for false and true(these indexes trade off being the active vs inactive variables, depending on whether the next index rightPtr is pointing to a block of false or true), along with how many changes are needed for each answer and the current amount of similar answers you can get in a row. Then check if the next block is less or equal to the activeK variable, if it is then the teacher can change all those answers so add that amount to the activeSum and take it away from activeK. If it is greater than the amount of changes left subtract the value in the activeLeftPtr and activeLeftPtr +1 from the activeSum and add activeLeftPtr +1 to the activeK (repeat until activeK > the rightPtr value or the activeLeftPtr has gone past rightPtr). Then check if any of the current sums + the changes they have leftover are a new best and continue. Return the minimum of the best and the length of the answersheet.
