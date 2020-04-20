## 1. Anagram Tester
```ruby
def anagram?(first_word, second_word)
  unless first_word.is_a?(String) && second_word.is_a?(String)
    return false
  end

  first_word.downcase.chars.sort == second_word.downcase.chars.sort
end
```

## 2. Anonymous Chat
```ruby
# config/routes.rb
Rails.application.routes.draw do
  resources :chats, only: [:new, :create] do 
    post 'add_message'
  end

  namespace :admin do
    resources :chats, only: [:index] do 
      post 'add_message'
      post 'mark_seen'
      post 'close'
    end
  end
end

```

## 3. Bug Fixing
**Common procedure**
- Check the log
- Try to re-generate the issue on Local environment
- Fix the issue
- Test the fix on Local/Testing environments
- If the issue is a major one (block a process or a page, stop users from using the system), we need to deploy the fix to Production as soon as possible
- If the issue is minor we might deploy it in the next release
- The issue is considered resolved when the fix has been deployed to Production and has been running stable for some period of time (several days, for example)

**Hard cases**
- Sometimes we have to take further actions to find out the root cause of the issues:
  * Extract some data from Production to Local to analyse (with limited access and caution)
  * Write more log around the case on Production 
- If the issue is critical and we cannot fix it quickly, we might have to roll back to the previous release

**Some practices**
- We should have a bug log to keep track of occured bugs for future references and improvements
- Keep customers informed with the progress/ actions we take if the issue takes a long time to fix

## 4. Taking over an old project
**Scenario 1**
- Assumptions:
  * The added business is not very imperative/ The deadline is not very tight 
  * (And/Or) The resource in hand is plentiful (resource to develop and to test)
- Actions
  * Study the old project and its correlation to new business cases
  * Adjust/Change the design so that it can support new cases with as least exceptional cases as possible
  
**Scenario 2**
- Assumptions:
  * The added business is imperative/ The deadline is tight
  * We are lack of resource
- Actions
  * Continue to finish the feature (might make more refactoring later)
  * Try to make the new code loose coupling from the old one
  * Might intentionally increase code duplication (to reduce the effect to the exising cases)

