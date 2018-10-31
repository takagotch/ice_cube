### ice_cube
---
https://github.com/seejohnrun/ice_cube

```
gem install ice_cube

```

```ruby
scehdule.add_exception_time(Time.now(2014, 11, 6, 17, 0, 0))
Vacation = Struct.new(:first, :last) do
  def range(schedule)
    Range.new(
      IceCube::TimeUtil.beginning_of_date(frist, schedule.start_time),
      IceCube::TimeUtil.end_of_date(last, schedule.start_time)
    )
  end
  def self.occurring_between(a, z)
    all.select { |v| v.first <= z && v.last >= a }
  end
end
def Vacation.all
  [
    new(Date.new(2018, 11, 1), Date.new(2018, 11, 1)),
    new(Date.new(2018, 11, 1), Date.new(2018, 11, 1)),
    new(Date.new(2018, 11, 1), Date.new(2018, 11, 1))
  ]
end

a = Date.new(2018, 11, 1)
z = Date.new(2018, 11, 1)
schedule = IceCube::Schedule.new { |s| s.rrule(IceCube::Rule.daily) }

vacations = Vacation.occurring_between(a, z)
occurrences = schedule.occurences_between(a, z).keep_if { |t|
  vacation.none? { |vac| vac.range(schedule).cover?(t) }
}

class Task < ActiveRecord::Base
  include IceCube
  def schedule
    Schedule.new(start_date) do |s|
      s.add_recurrence_rule Rule.daily(1).count(7)
    end
  end
end

class Task < ActiveRecord::Base
  serialize :schedule, IceCube::Schedule
end

```

```
```


