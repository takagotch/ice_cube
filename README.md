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

```ruby
schedule = IceCube::Schedule.new
schedule.add_recurrence_rule(
  IceCube::Rule.yearly.day_of_month(13).day(:friday).month_of_year(:october)
)

schedule = IceCube::Schedule.new(now = Time.now) do |s|
  s.add_recurrence_rule(IceCube::Rule.daily.count(4))
  s.add_exception_time(now + 1.day)
end

occurrences = schedule.occurrences(end_time)
occurrences = schedule.all_occurrences
schedule.occurs_at?(now + 1.day)
schedule.occurs_at?(now + 2.days)
schedule.occurs_on?(Date.today)
schedule.occurs_between?(now, now + 30.days)
schedule.occurs_between?(now + 4.days, now + 30.days)
schedule.first(2)
schedule.first
schedule.last(2)
schedule.last

schedule.next_occurrence(from_time)
schedule.next_occurrence(4, from_time)
schedule.remaining_occurrences

schedule.previous_occurrence(from_time)
schedule.previous_occurrences(4, from_time)

schedule.next_occurrences(4, from_time, :spans => true)
schedule.occurrences_between(from_time, to_time, :spans => true)

schedule = IceCube::Schedule.new(now, :duration => 3600)
schedule.add_recurrence_rule IceCube::Rule.daily
schedule.occurring_at?(now + 1800)
schedule.occurring_between?(t1, t2)

schedule = IceCube::Schedule.new(start = Time.now, :end_time => start + 3600)
schedule.add_recurrence_rule IceCube::Rule.daily
schedule.occurring_at?(start + 3599)
schedule.occuring_at?(start + 3600)

schedule = IceCube::Schedule.new
schedule.add_recurrence_rule IceCube::Rule.daily.until(Date.today + 30)
schedule.each_occurrence { |t| puts t}

yaml = schedule.to_yaml
IceCube::Schedule.from_yaml(yaml)

hash = schedule.to_hash
IceCube::Schedule.from_hash(hash)

ical = schedule.to_ical
IceCube::Schedule.from_ical(ical)

rule = IceCube::Rule.daily(2).day_of_week(:tuesday => [1, -1], :wednesday => [2])
rule.to_ical
rule.to_s

schdule.add_recurrence_rule IceCube::Rule.daily
schedule.add_recurrence_rule IceCube::Rule.daily(3)

schedule.add_recurrence_rule IceCube::Rule.weekly
schedule.add_recurrence_rule IceCube::Rule.weekly(2).day(:monday, :tuesday)
schedule.add_recurrence_rule IceCube::Rule.weekly(2).day(1, 2)
schedule.add_recurrence_rule IceCube::Rule.weekly(1, :monday)

schedule.add_recurrence_rule IceCube::Rule.monthly.day_of_month(1, -1)
schedule.add_recurrence_rule IceCube::Rule.monthly(2).day_of_month(15)


```


