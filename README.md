Use Full Links: https://pub.dev/





অবশ্যই\! আমি আপনার দেওয়া সম্পূর্ণ কোডটি লাইন বাই লাইন বা অংশ অনুযায়ী সহজ বাংলায় ব্যাখ্যা করে দিচ্ছি।

-----

### \#\#\# ১. Import Statements (প্রয়োজনীয় প্যাকেজ ইমপোর্ট)

```dart
import 'package.flutter/material.dart';
import 'package.table_calendar/table_calendar.dart';
// Note: নিচের লাইনটিতে একটি ভুল আছে, এটি google_fonts/google_fonts.dart হবে
import 'package.google_fonts/google_fonts.dart';
```

  * **`material.dart`**: Flutter-এর সব বেসিক ডিজাইন উইজেট (যেমন `Scaffold`, `AppBar`, `Text` ইত্যাদি) ব্যবহার করার জন্য এটি ইমপোর্ট করা হয়।
  * **`table_calendar.dart`**: `TableCalendar` উইজেটটি, যা দিয়ে আমরা ক্যালেন্ডারটি বানিয়েছি, সেটি ব্যবহার করার জন্য এই প্যাকেজটি ইমপোর্ট করা হয়েছে।
  * **`google_fonts.dart`**: Google Fonts থেকে বিভিন্ন স্টাইলিশ ফন্ট ব্যবহার করার জন্য এটি ইমপোর্ট করা হয়।

-----

### \#\#\# ২. `StatefulWidget` তৈরি করা

```dart
class MyCalendar extends StatefulWidget {
  const MyCalendar({super.key});

  @override
  State<MyCalendar> createState() => _MyCalendarState();
}
```

  * **`class MyCalendar extends StatefulWidget`**: এখানে `MyCalendar` নামে একটি `StatefulWidget` তৈরি করা হচ্ছে। `StatefulWidget` হলো এমন উইজেট যার ভেতরের ডেটা বা অবস্থা (state) সময়ের সাথে পরিবর্তন হতে পারে (যেমন: ব্যবহারকারী একটি নতুন তারিখ সিলেক্ট করলে UI পরিবর্তন হবে)।
  * **`createState()`**: এই মেথডটি `_MyCalendarState` ক্লাসটিকে তৈরি করে এবং `StatefulWidget`-এর সাথে যুক্ত করে। মূল UI এবং সব পরিবর্তনশীল ডেটা এই `_MyCalendarState` ক্লাসের ভেতরেই থাকে।

-----

### \#\#\# ৩. `_MyCalendarState` ক্লাস (মূল UI ও ডেটা)

```dart
class _MyCalendarState extends State<MyCalendar> {
  DateTime _focusedDay = DateTime.now();
  DateTime? _selectedDay;

  @override
  void initState() {
    super.initState();
    _selectedDay = _focusedDay;
  }
  // ... বাকি কোড
}
```

  * **`DateTime _focusedDay = DateTime.now()`**: `_focusedDay` নামে একটি ভ্যারিয়েবল, যা ক্যালেন্ডারটি বর্তমানে কোন মাস দেখাচ্ছে তা নিয়ন্ত্রণ করে। প্রাথমিকভাবে এর মান `DateTime.now()` দেওয়া হয়েছে, অর্থাৎ অ্যাপটি খুললে আজকের মাসটিই দেখাবে।
  * **`DateTime? _selectedDay`**: `_selectedDay` নামে আরেকটি ভ্যারিয়েबल, যা ব্যবহারকারীর সিলেক্ট করা তারিখটি সংরক্ষণ করে। `?` চিহ্ন দিয়ে বোঝানো হচ্ছে যে এর মান খালি (`null`) থাকতে পারে।
  * **`initState()`**: এই মেথডটি পেইজটি তৈরি হওয়ার সময় মাত্র একবারই রান হয়।
  * **`_selectedDay = _focusedDay`**: `initState`-এর ভেতরে এই লাইনটির মাধ্যমে আমরা প্রাথমিকভাবে সিলেক্ট করা দিন হিসেবে আজকের তারিখটিকে সেট করে দিচ্ছি, যাতে ক্যালেন্ডার খুললেই আজকের দিনটি সিলেক্টেড থাকে।

-----

### \#\#\# ৪. `_setReminder()` ফাংশন

```dart
void _setReminder() {
  if (_selectedDay != null) {
    showDialog(...);
  } else {
    ScaffoldMessenger.of(context).showSnackBar(...);
  }
}
```

  * এটি একটি ফাংশন যা "Set Reminder" বাটনে চাপ দিলে কাজ করে।
  * **`if (_selectedDay != null)`**: এটি চেক করে দেখে যে ব্যবহারকারী কোনো তারিখ সিলেক্ট করেছে কি না।
  * **`showDialog(...)`**: যদি কোনো তারিখ সিলেক্ট করা থাকে, তাহলে এটি একটি পপ-আপ মেসেজ (`AlertDialog`) দেখায়।
  * **`ScaffoldMessenger...`**: যদি কোনো তারিখ সিলেক্ট করা না থাকে, তাহলে এটি স্ক্রিনের নিচে একটি অস্থায়ী মেসেজ (`SnackBar`) দেখায়।

-----

### \#\#\# ৫. `build()` মেথড (UI তৈরি করা)

```dart
@override
Widget build(BuildContext context) {
  return Scaffold(...);
}
```

এই মেথডটি আপনার পেইজের সম্পূর্ণ UI বা দৃশ্যমান অংশটি তৈরি করে।

  * **`Scaffold`**: এটি যেকোনো পেইজের মূল কাঠামো। এর মধ্যে `AppBar` (উপরের বার) এবং `body` (মূল অংশ) থাকে।
  * **`AppBar`**: পেইজের উপরের বার।
      * **`title: Text('Set Date')`**: AppBar-এর টাইটেল সেট করে।
      * **`actions: [...]`**: AppBar-এর ডান পাশে আইকন বা বাটন যুক্ত করে।
      * **`IconButton(...)`**: একটি ক্লিক করার মতো আইকন বাটন (এখানে টিক ✔ চিহ্ন)।
      * **`Navigator.pop(context, _selectedDay)`**: এই বাটনে চাপ দিলে বর্তমান পেইজটি বন্ধ হয়ে যাবে এবং সিলেক্ট করা তারিখটি (`_selectedDay`) আগের পেইজে ফেরত যাবে।
  * **`Padding`**: `body`-র ভেতরে চারিদিকে ১৬ পিক্সেলের একটি খালি জায়গা তৈরি করে, যাতে ডিজাইনটি সুন্দর দেখায়।
  * **`Column`**: এর ভেতরের উইজেটগুলোকে একটার নিচে একটা করে সাজিয়ে রাখে।
  * **`TableCalendar(...)`**: এটি মূল ক্যালেন্ডার উইজেট।
      * **`focusedDay: _focusedDay`**: ক্যালেন্ডার কোন মাস দেখাবে তা নিয়ন্ত্রণ করে।
      * **`selectedDayPredicate: (day) => isSameDay(_selectedDay, day)`**: কোন দিনটি সিলেক্টেড হিসেবে হাইলাইট হবে তা নির্ধারণ করে।
      * **`onDaySelected: (selectedDay, focusedDay) { ... }`**: যখন ব্যবহারকারী কোনো দিনের ওপর ট্যাপ করে, তখন এই ফাংশনটি কাজ করে।
      * **`setState(() { ... })`**: এটি Flutter-কে জানায় যে ডেটা পরিবর্তন হয়েছে, তাই UI আবার নতুন করে তৈরি করতে হবে। এখানে আমরা `_selectedDay`-এর মান পরিবর্তন করে UI আপডেট করি।
  * **`Spacer()`**: এটি `Column`-এর ভেতরে থাকা দুটি উইজেটের মাঝের সবটুকু খালি জায়গা নিয়ে নেয়। ফলে "Set Reminder" বাটনটি একদম নিচে চলে যায়।
  * **`ElevatedButton.icon(...)`**: এটি "Set Reminder" বাটন।
      * **`onPressed: _setReminder`**: এই বাটনে চাপ দিলে উপরে বানানো `_setReminder` ফাংশনটি কল হবে।


      











সহজ কথায়, যে উইজেটের চেহারা বা ডেটা **কখনো পরিবর্তন হয় না**, তার জন্য **StatelessWidget** ব্যবহার করা হয়। আর যে উইজেটের চেহারা বা ডেটা ব্যবহারকারীর কোনো কাজের ফলে বা অন্য কোনো কারণে **পরিবর্তন হতে পারে**, তার জন্য **StatefulWidget** ব্যবহার করা হয়।

নিচে বিস্তারিতভাবে আলোচনা করা হলো।

-----

### \#\# 🧊 StatelessWidget (পরিবর্তনহীন উইজেট)

এটা অনেকটা একটা **প্রিন্ট করা ছবির** মতো। একবার তৈরি হয়ে গেলে এর ভেতরের কোনো কিছু আর পরিবর্তন করা যায় না। এটি শুধু ডেটা গ্রহণ করে এবং সেই অনুযায়ী UI দেখায়।

**কখন ব্যবহার করবেন?**
যখন আপনার উইজেটটি স্ক্রিনে আসার পর এর আর কোনো পরিবর্তন হওয়ার দরকার নেই।

  * **বৈশিষ্ট্য:**

      * এর অবস্থা বা **state পরিবর্তন করা যায় না (immutable)**।
      * এটি শুধুমাত্র `build` মেথড ব্যবহার করে UI তৈরি করে।
      * এতে `setState()` মেথড নেই, কারণ এর অবস্থা পরিবর্তন করার কোনো প্রয়োজনই হয় না।

  * **উদাহরণ:**

      * `Icon`, `Text`, `Image` ইত্যাদি।
      * একটি ওয়েলকাম স্ক্রিন যেখানে শুধু লেখা এবং ছবি আছে।
      * একটি "About Us" পেইজ, যেখানে তথ্যগুলো স্থির থাকে।
      * অ্যাপের লোগো দেখানো।

**কোড উদাহরণ:**

```dart
class WelcomeMessage extends StatelessWidget {
  final String userName;

  const WelcomeMessage({super.key, required this.userName});

  @override
  Widget build(BuildContext context) {
    // এখানে userName পরিবর্তন করার কোনো উপায় নেই
    return Text(
      'Hello, $userName!',
      style: TextStyle(fontSize: 24),
    );
  }
}
```

-----

### \#\# 🎭 StatefulWidget (পরিবর্তনশীল উইজেট)

এটা অনেকটা একটি **হোয়াইটবোর্ডের** মতো, যেখানে আপনি যখন ইচ্ছা নতুন কিছু আঁকতে বা মুছতে পারেন। অর্থাৎ, এর ভেতরের ডেটা বা অবস্থা পরিবর্তন হতে পারে এবং সেই পরিবর্তনের সাথে সাথে এর UI-ও পরিবর্তন হয়।

**কখন ব্যবহার করবেন?**
যখন ব্যবহারকারীর কোনো কাজের (যেমন: বাটন ক্লিক, লেখা টাইপ করা) ফলে বা অন্য কোনো কারণে উইজেটের চেহারা বা ডেটা পরিবর্তন করতে হবে।

  * **বৈশিষ্ট্য:**

      * এর অবস্থা বা **state পরিবর্তন করা যায় (mutable)**।
      * এটি দুটি ক্লাস নিয়ে গঠিত: একটি `Widget` ক্লাস এবং একটি `State` ক্লাস। মূল পরিবর্তনগুলো `State` ক্লাসের ভেতরে হয়।
      * UI পরিবর্তন করার জন্য **`setState()`** মেথড কল করতে হয়। `setState()` কল করা হলে `build` মেথডটি আবার রান হয় এবং নতুন ডেটা অনুযায়ী UI আপডেট করে।

  * **উদাহরণ:**

      * একটি `Checkbox` যা টিক দেওয়া বা ওঠানো যায়।
      * একটি `TextField` যেখানে ব্যবহারকারী কিছু টাইপ করতে পারে।
      * একটি কাউন্টার অ্যাপ, যেখানে বাটনে ক্লিক করলে সংখ্যা বাড়ে।
      * একটি পেইজ যা ইন্টারনেট থেকে ডেটা লোড করে দেখায় (প্রথমে লোডিং, পরে ডেটা)।
      * আমরা যে ক্যালেন্ডারটি বানিয়েছি, কারণ সেখানে সিলেক্ট করা দিন পরিবর্তন হয়।

**কোড উদাহরণ:**

```dart
class Counter extends StatefulWidget {
  const Counter({super.key});

  @override
  State<Counter> createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _count = 0; // এই ডেটাটি পরিবর্তন হবে

  void _increment() {
    // setState কল করার ফলে UI আপডেট হবে
    setState(() {
      _count++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Count: $_count', style: TextStyle(fontSize: 24)),
        ElevatedButton(
          onPressed: _increment,
          child: Text('Add'),
        ),
      ],
    );
  }
}
```

-----

### \#\# এক নজরে পার্থক্য

| বিষয় (Topic)      | StatelessWidget                           | StatefulWidget                           |
| ----------------- | ------------------------------------------ | ---------------------------------------- |
| **অবস্থা (State)** | পরিবর্তন হয় না (Immutable)                  | পরিবর্তন হয় (Mutable)                      |
| **UI আপডেট** | নিজে করতে পারে না, প্যারেন্ট থেকে ডেটা পায়   | `setState()` মেথড দিয়ে নিজে আপডেট করে    |
| **ব্যবহার** | স্ট্যাটিক UI, যা পরিবর্তন হবে না         | ডাইনামিক UI, যা পরিবর্তন হবে           |
| **উদাহরণ** | `Icon`, `Text`, `Container`                  | `Checkbox`, `TextField`, `Slider`          |

### \#\# সহজ নিয়ম

নিজেকে প্রশ্ন করুন: **"এই উইজেটের জীবদ্দশায় কি এর ভেতরের কোনো ডেটা পরিবর্তন হবে?"**

  * যদি উত্তর **'না'** হয়, তাহলে **StatelessWidget** ব্যবহার করুন।
  * যদি উত্তর **'হ্যাঁ'** হয়, তাহলে **StatefulWidget** ব্যবহার করুন।
