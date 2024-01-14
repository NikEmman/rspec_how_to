# How to short hand tests

```rb
describe User do
  subject { User.new("Francisca", "#{year}-01-01") }

  context "born in 2001" do
    let(:year) { 2001 }
    it { should_not be_born_in_leap_year }
  end

  context "born in 1900" do
    let(:year) { 1900 }
    it { should_not be_born_in_leap_year }
  end

  context "born in 2000" do
    let(:year) { 2000 }
    it { should be_born_in_leap_year }
  end

  context "born in 2004" do
    let(:year) { 2004 }
    it { should be_born_in_leap_year }
  end
end
```
##To summarize, the extra features used are:

- Let allows you to dynamically define a method that will return the given value. We use this to define the only varying bit of data: the year. It is important to note that let memoizes the result. I.e. it only calls the block once. Also, it only executes the block when you actually call it.
- Subject is a convenience helper that lets us specify the “thing” that is under test. In our case that’s a User instance. subject also memoizes the result. And just like let, it also only executes the block when you actually call it.
- Should assumes that we want to test the subject. It is a shorthand for expect(subject).to (while should_not is the corresponding shorthand for expect(subject).not_to).
- `be_born_in_leap_year` uses the `#born_in_leap_year?` method defined in `User` class.
