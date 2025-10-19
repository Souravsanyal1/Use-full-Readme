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



  Flutter-এর `AppBar`-এ আপনি মূলত তিনটি প্রধান অংশে উইজেট যোগ করতে পারেন: **leading** (বাম পাশে), **title** (মাঝখানে), এবং **actions** (ডান পাশে)। এছাড়াও এর ডিজাইন ও কার্যকারিতা পরিবর্তন করার জন্য অনেক অপশন আছে।

নিচে বিস্তারিতভাবে আলোচনা করা হলো।

-----

### \#\# ✍️ প্রধান উইজেটগুলো

1.  **`leading`**: এটি `AppBar`-এর একদম বাম পাশের উইজেট। সাধারণত এখানে মেনু আইকন (drawer) বা আগের পেইজে ফেরত যাওয়ার back button থাকে।

    ```dart
    leading: Icon(Icons.menu),
    ```

2.  **`title`**: এটি `AppBar`-এর প্রধান অংশ, যা সাধারণত অ্যাপের নাম বা বর্তমান পেইজের নাম দেখায়। `title` হিসেবে শুধু `Text` নয়, যেকোনো উইজেট (যেমন: `Image`, `Row`) ব্যবহার করা যায়।

    ```dart
    title: Text('My App'),
    ```

3.  **`actions`**: এটি একটি তালিকা (`List`) যেখানে আপনি `AppBar`-এর ডান পাশে এক বা একাধিক উইজেট (সাধারণত `IconButton`) যোগ করতে পারেন। যেমন: সার্চ, নোটিফিকেশন, সেটিংস বা প্রোফাইল বাটন।

    ```dart
    actions: [
      IconButton(icon: Icon(Icons.search), onPressed: () {}),
      IconButton(icon: Icon(Icons.more_vert), onPressed: () {}),
    ],
    ```

-----

### \#\# 🎨 ডিজাইন ও অন্যান্য প্রোপার্টি

1.  **`backgroundColor`**: `AppBar`-এর الخلفية রঙ পরিবর্তন করার জন্য এটি ব্যবহার করা হয়।

    ```dart
    backgroundColor: Colors.teal,
    ```

2.  **`elevation`**: `AppBar`-এর নিচে ছায়া (shadow) কতটা গভীর হবে তা নিয়ন্ত্রণ করে। মান `0` দিলে কোনো ছায়া থাকবে না।

    ```dart
    elevation: 4.0,
    ```

3.  **`centerTitle`**: `title`-কে মাঝখানে দেখানোর জন্য এটি `true` সেট করতে হয়। ডিফল্টভাবে এটি Android-এ `false` এবং iOS-এ `true` থাকে।

    ```dart
    centerTitle: true,
    ```

4.  **`shape`**: `AppBar`-এর আকৃতি পরিবর্তন করার জন্য এটি ব্যবহার করা হয়। যেমন, নিচের কোণাগুলো গোলাকার করার জন্য।

    ```dart
    shape: RoundedRectangleBorder(
      borderRadius: BorderRadius.vertical(
        bottom: Radius.circular(20),
      ),
    ),
    ```

5.  **`bottom`**: `AppBar`-এর ঠিক নিচে আরেকটি উইজেট যোগ করার জন্য এটি ব্যবহার করা হয়। সাধারণত `TabBar` দেখানোর জন্য এটি সবচেয়ে বেশি ব্যবহৃত হয়।

    ```dart
    bottom: TabBar(
      tabs: [
        Tab(icon: Icon(Icons.home)),
        Tab(icon: Icon(Icons.settings)),
      ],
    ),
    ```

6.  **`flexibleSpace`**: `AppBar`-এর الخلفية তে কোনো ছবি বা গ্র্যাডিয়েন্ট রঙ দেখানোর জন্য এটি ব্যবহার করা হয়। স্ক্রল করার সাথে সাথে এটি সুন্দর ইফেক্ট তৈরি করে।

    ```dart
    flexibleSpace: Container(
      decoration: BoxDecoration(
        gradient: LinearGradient(
          colors: [Colors.blue, Colors.purple],
          begin: Alignment.bottomRight,
          end: Alignment.topLeft,
        ),
      ),
    ),
    ```

-----

### \#\# কোড উদাহরণ

নিচে উপরের সবগুলো বৈশিষ্ট্য ব্যবহার করে একটি সম্পূর্ণ `AppBar`-এর উদাহরণ দেওয়া হলো:

```dart
import 'package:flutter/material.dart';

class MyAppBarExample extends StatelessWidget {
  const MyAppBarExample({super.key});

  @override
  Widget build(BuildContext context) {
    return DefaultTabController(
      length: 2, // Tab সংখ্যা
      child: Scaffold(
        appBar: AppBar(
          // ১. বাম পাশের আইকন
          leading: IconButton(
            icon: Icon(Icons.menu),
            onPressed: () {},
          ),
          // ২. টাইটেল
          title: Text('Advanced AppBar'),
          // ৩. টাইটেলকে মাঝখানে আনা
          centerTitle: true,
          // ৪. الخلفية রঙ
          backgroundColor: Colors.indigo,
          // ৫. ডান পাশের বাটনগুলো
          actions: [
            IconButton(icon: Icon(Icons.search), onPressed: () {}),
            IconButton(icon: Icon(Icons.notifications_none), onPressed: () {}),
          ],
          // ৬. নিচের ছায়া
          elevation: 8.0,
          // ৭. AppBar এর নিচে TabBar যোগ করা
          bottom: TabBar(
            tabs: [
              Tab(text: 'Home', icon: Icon(Icons.home)),
              Tab(text: 'Profile', icon: Icon(Icons.person)),
            ],
          ),
          // ৮. AppBar এর আকৃতি পরিবর্তন
          shape: RoundedRectangleBorder(
            borderRadius: BorderRadius.vertical(
              bottom: Radius.circular(25),
            ),
          ),
        ),
        body: TabBarView(
          // TabBarView এর ভেতরে Tab অনুযায়ী পেইজ দেখানো হয়
          children: [
            Center(child: Text('Home Page')),
            Center(child: Text('Profile Page')),
          ],
        ),
      ),
    );
  }
}
```



Flutter-এ `Icon`, `Text`, এবং `Image` হলো 가장 বেশি ব্যবহৃত উইজেটগুলোর মধ্যে তিনটি। নিচে এগুলোর ব্যবহার সহজ বাংলায় ব্যাখ্যা করা হলো।

-----

### \#\# 📌 Icon উইজেট

এটি Material Design-এর প্রি-ডিফাইন্ড আইকনগুলো দেখানোর জন্য ব্যবহার করা হয়।

**কখন ব্যবহার করবেন?**
যখন কোনো প্রতীক বা চিহ্ন দেখাতে হবে, যেমন: মেনু, সার্চ, প্রোফাইল বাটন ইত্যাদি।

  * **বেসিক ব্যবহার:**

    ```dart
    Icon(Icons.home) // একটি বাড়ি আইকন দেখাবে
    ```

  * **প্রধান প্রোপার্টি:**

      * **`size`**: আইকনের আকার ছোট বা বড় করার জন্য।
      * **`color`**: আইকনের রঙ পরিবর্তন করার জন্য।

  * **কোড উদাহরণ:**

    ```dart
    Center(
      child: Icon(
        Icons.favorite,      // قلب আইকন
        size: 50.0,           // আকার 50 পিক্সেল
        color: Colors.red,    // রঙ লাল
      ),
    )
    ```

-----

### \#\# ✍️ Text উইজেট

যেকোনো লেখা বা স্ট্রিং স্ক্রিনে দেখানোর জন্য `Text` উইজেট ব্যবহার করা হয়।

**কখন ব্যবহার করবেন?**
যখন কোনো শিরোনাম, বর্ণনা, বা যেকোনো ধরনের লেখা দেখাতে হবে।

  * **বেসিক ব্যবহার:**

    ```dart
    Text('Hello, Flutter!')
    ```

  * **প্রধান প্রোপার্টি:**

      * **`style`**: লেখার স্টাইল পরিবর্তন করার জন্য এটি `TextStyle` গ্রহণ করে। এর মাধ্যমে আপনি `fontSize`, `color`, `fontWeight` (লেখা মোটা করা) ইত্যাদি পরিবর্তন করতে পারবেন।

  * **কোড উদাহরণ:**

    ```dart
    Center(
      child: Text(
        'This is a sample text.',
        textAlign: TextAlign.center, // লেখাটিকে মাঝখানে আনার জন্য
        style: TextStyle(
          fontSize: 24.0,                 // ফন্টের আকার
          color: Colors.blue,             // ফন্টের রঙ
          fontWeight: FontWeight.bold,    // লেখাটিকে বোল্ড করবে
          fontStyle: FontStyle.italic,    // লেখাটিকে ইটালিক করবে
        ),
      ),
    )
    ```

-----

### \#\# 🖼️ Image উইজেট

ছবি দেখানোর জন্য `Image` উইজেট ব্যবহার করা হয়। ছবি দেখানোর কয়েকটি জনপ্রিয় উপায় আছে।

**কখন ব্যবহার করবেন?**
যখন অ্যাপের ভেতরে থাকা কোনো ছবি, ইন্টারনেট থেকে আনা ছবি, বা ব্যবহারকারীর ফোনের ছবি দেখাতে হবে।

#### **১. `Image.asset()` (প্রজেক্টের ভেতরের ছবি)**

প্রজেক্টের `assets` ফোল্ডারে রাখা ছবি দেখানোর জন্য এটি ব্যবহার করা হয়।

  * **ব্যবহারের ধাপ:**

    1.  আপনার প্রজেক্টের রুটে `assets` নামে একটি ফোল্ডার তৈরি করুন এবং তার ভেতরে আপনার ছবিটি রাখুন (যেমন: `assets/my_image.png`)।
    2.  `pubspec.yaml` ফাইলে গিয়ে `assets` ফোল্ডারটি declare করুন:
        ```yaml
        flutter:
          uses-material-design: true
          assets:
            - assets/
        ```
    3.  এবার কোডে ব্যবহার করুন।

  * **কোড উদাহরণ:**

    ```dart
    Image.asset(
      'assets/my_image.png',
      width: 150,
      height: 150,
      fit: BoxFit.cover, // ছবিটি যেন সুন্দরভাবে ফ্রেমের সাথে ফিট হয়
    )
    ```

#### **২. `Image.network()` (ইন্টারনেটের ছবি)**

সরাসরি কোনো URL থেকে ছবি দেখানোর জন্য এটি ব্যবহার করা হয়।

  * **কোড উদাহরণ:**
    ```dart
    Image.network(
      'https://flutter.dev/images/flutter-logo-sharing.png',
      width: 200,
      height: 200,
      loadingBuilder: (context, child, progress) {
        return progress == null ? child : CircularProgressIndicator();
      },
    )
    ```

এই তিনটি উইজেট ব্যবহার করেই আপনি যেকোনো অ্যাপের বেসিক UI ডিজাইন করে ফেলতে পারবেন।



সহজ কথায়, Flutter-এ `child` প্রোপার্টির ভেতরে **যেকোনো একটি উইজেট (any single Widget)** দেওয়া যায়।

এটা অনেকটা একটি বাক্সের মতো, যার ভেতরে আপনি মাত্র **একটি জিনিস** রাখতে পারবেন। সেই জিনিসটি হতে পারে একটি `Text`, একটি `Icon`, একটি `Image`, অথবা এমনকি আরেকটি `Container`।

**উদাহরণ (Single-Child Widgets):**
`Container`, `Center`, `Padding`, `Card`, `SizedBox` ইত্যাদি উইজেটগুলোর একটি `child` থাকে।

```dart
// Container-এর child হিসেবে একটি Text উইজেট
Container(
  color: Colors.blue,
  child: Text('Hello'), // <-- একটি মাত্র উইজেট
)

// Center-এর child হিসেবে একটি Icon উইজেট
Center(
  child: Icon(Icons.home), // <-- একটি মাত্র উইজেট
)
```

-----

### \#\# যদি একাধিক উইজেট যোগ করতে হয়? (Using `children`)

যখন আপনার একটির বেশি উইজেট (যেমন: একটি আইকন এবং তার পাশের লেখা) পাশাপাশি বা একটার নিচে আরেকটা রাখতে হবে, তখন আপনি এমন উইজেট ব্যবহার করবেন যার `child` নয়, বরং **`children`** প্রোপার্টি আছে।

`children` প্রোপার্টি একটি **উইজেটের তালিকা (List of Widgets)** গ্রহণ করে।

**উদাহরণ (Multi-Child Widgets):**
`Row`, `Column`, `ListView`, `Stack`, `GridView` ইত্যাদি উইজেটগুলোর `children` প্রোপার্টি থাকে।

```dart
// Row-এর children হিসেবে একটি Icon এবং একটি Text
Row(
  children: [ // <-- children একটি List গ্রহণ করে
    Icon(Icons.star),
    SizedBox(width: 8),
    Text('Rating: 4.5'),
  ],
)

// Column-এর children হিসেবে একটি Image এবং একটি Text
Column(
  children: [ // <-- children একটি List গ্রহণ করে
    Image.asset('assets/profile.png'),
    Text('User Name'),
  ],
)
```

-----

### \#\# উইজেট নেস্টিং (Nesting)

Flutter-এর আসল শক্তি হলো উইজেটগুলোকে একটির ভেতরে আরেকটি বসানো (nesting)। আপনি একটি `child` থাকা উইজেটের ভেতরে `children` থাকা উইজেট বসাতে পারেন।

**উদাহরণ:**
একটি `Container`-এর `child` হিসেবে একটি `Column` ব্যবহার করা, যার `children` হিসেবে আবার একাধিক `Text` ও `Icon` আছে।

```dart
Center(
  child: Container(
    padding: EdgeInsets.all(16.0),
    decoration: BoxDecoration(
      color: Colors.grey[200],
      borderRadius: BorderRadius.circular(12),
    ),
    // Container-এর একটি মাত্র child
    child: Column( // <-- child হিসেবে Column ব্যবহার করা হয়েছে
      mainAxisSize: MainAxisSize.min,
      // Column-এর একাধিক children
      children: [
        Icon(Icons.check_circle, color: Colors.green, size: 40),
        SizedBox(height: 10),
        Text('Payment Successful!', style: TextStyle(fontSize: 20)),
      ],
    ),
  ),
)
```

### সারসংক্ষেপ:

  * **`child`**: এর ভেতরে **একটি** উইজেট দেওয়া যায়।
  * **`children`**: এর ভেতরে **একাধিক** উইজেট (একটি `List`-এর মধ্যে) দেওয়া যায়।


সহজ কথায়, **Row** উইজেট ব্যবহার করা হয় একাধিক জিনিসকে **পাশাপাশি** সাজানোর জন্য, আর **Column** ব্যবহার করা হয় জিনিসগুলোকে **একটির নিচে একটি করে** সাজানোর জন্য।

এরা Flutter-এর দুটি মৌলিক লেআউট উইজেট। নিচে এদের কাজ এবং বৈশিষ্ট্য বিস্তারিতভাবে আলোচনা করা হলো।

-----

### \#\# ➡️ Row উইজেট

**কখন ব্যবহার হয়?**
যখন আপনাকে আইকন, টেক্সট, বাটন বা অন্য যেকোনো উইজেটকে বাম থেকে ডানে অর্থাৎ পাশাপাশি সাজাতে হয়।

**কীভাবে কাজ করে?**
`Row` তার `children` তালিকার মধ্যে থাকা সব উইজেটকে একটি অনুভূমিক (horizontal) লাইনে সাজিয়ে দেয়।

**প্রধান প্রোপার্টিগুলো:**

1.  **`children`**: এটি একটি উইজেটের তালিকা (`List<Widget>`) গ্রহণ করে, যেগুলোকে পাশাপাশি দেখানো হবে।

2.  **`mainAxisAlignment`**: `Row`-এর মূল অক্ষ হলো অনুভূমিক (horizontal)। এই অক্ষ বরাবর উইজেটগুলো কীভাবে সাজানো থাকবে, তা `mainAxisAlignment` দিয়ে ঠিক করা হয়। এর কিছু জনপ্রিয় মান হলো:

      * **`MainAxisAlignment.start`**: উইজেটগুলোকে একদম বাম পাশ থেকে শুরু করে। (ডিফল্ট)
      * **`MainAxisAlignment.center`**: উইজেটগুলোকে মাঝখানে নিয়ে আসে।
      * **`MainAxisAlignment.end`**: উইজেটগুলোকে একদম ডান পাশে নিয়ে যায়।
      * **`MainAxisAlignment.spaceBetween`**: প্রথম ও শেষ উইজেটকে দুই প্রান্তে রেখে বাকিগুলোকে সমান ফাঁকা জায়গায় ভাগ করে দেয়।
      * **`MainAxisAlignment.spaceAround`**: প্রত্যেক উইজেটের দুই পাশে সমান জায়গা রাখে।
      * **`MainAxisAlignment.spaceEvenly`**: সব উইজেটের মাঝে এবং দুই প্রান্তে সমান জায়গা রাখে।

3.  **`crossAxisAlignment`**: `Row`-এর আড়াআড়ি অক্ষ হলো উল্লম্ব (vertical)। এই অক্ষ বরাবর উইজেটগুলো কীভাবে সাজানো থাকবে, তা `crossAxisAlignment` দিয়ে ঠিক করা হয়।

      * **`CrossAxisAlignment.start`**: উইজেটগুলোকে উপরের দিকে অ্যালাইন করে।
      * **`CrossAxisAlignment.center`**: উইজেটগুলোকে উল্লম্বভাবে মাঝখানে রাখে। (ডিফল্ট)
      * **`CrossAxisAlignment.end`**: উইজেটগুলোকে নিচের দিকে অ্যালাইন করে।
      * **`CrossAxisAlignment.stretch`**: উইজেটগুলোকে পুরো `Row`-এর উচ্চতা জুড়ে প্রসারিত করে।

**কোড উদাহরণ:**

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.spaceAround, // মাঝখানে সমান ফাঁকা জায়গা
  crossAxisAlignment: CrossAxisAlignment.center, // উল্লম্বভাবে মাঝখানে
  children: [
    Icon(Icons.star, size: 50),
    Icon(Icons.star, size: 50),
    Icon(Icons.star, size: 50),
  ],
)
```

-----

### \#\# ⬇️ Column উইজেট

**কখন ব্যবহার হয়?**
যখন আপনাকে উইজেটগুলোকে উপর থেকে নিচে অর্থাৎ একটির নিচে একটি করে সাজাতে হয়।

**কীভাবে কাজ করে?**
`Column` তার `children` তালিকার মধ্যে থাকা সব উইজেটকে একটি উল্লম্ব (vertical) লাইনে সাজিয়ে দেয়।

**প্রধান প্রোপার্টিগুলো:**

1.  **`children`**: এটি একটি উইজেটের তালিকা (`List<Widget>`) গ্রহণ করে, যেগুলোকে উপর-নিচ করে দেখানো হবে।

2.  **`mainAxisAlignment`**: `Column`-এর মূল অক্ষ হলো উল্লম্ব (vertical)। এই অক্ষ বরাবর উইজেটগুলো কীভাবে সাজানো থাকবে, তা `mainAxisAlignment` দিয়ে ঠিক করা হয় (যেমন: `start`, `center`, `spaceBetween` ইত্যাদি)।

3.  **`crossAxisAlignment`**: `Column`-এর আড়াআড়ি অক্ষ হলো অনুভূমিক (horizontal)। এই অক্ষ বরাবর উইজেটগুলো কীভাবে সাজানো থাকবে, তা `crossAxisAlignment` দিয়ে ঠিক করা হয়।

      * **`CrossAxisAlignment.start`**: উইজেটগুলোকে বাম দিকে অ্যালাইন করে।
      * **`CrossAxisAlignment.center`**: উইজেটগুলোকে অনুভূমিকভাবে মাঝখানে রাখে। (ডিফল্ট)
      * **`CrossAxisAlignment.end`**: উইজেটগুলোকে ডান দিকে অ্যালাইন করে।
      * **`CrossAxisAlignment.stretch`**: উইজেটগুলোকে পুরো `Column`-এর প্রস্থ জুড়ে প্রসারিত করে।

**কোড উদাহরণ:**

```dart
Column(
  mainAxisAlignment: MainAxisAlignment.center, // উল্লম্বভাবে মাঝখানে
  crossAxisAlignment: CrossAxisAlignment.start, // অনুভূমিকভাবে বাম দিক থেকে
  children: [
    Text('First Item', style: TextStyle(fontSize: 24)),
    Text('Second Item', style: TextStyle(fontSize: 24)),
    Text('Third Item', style: TextStyle(fontSize: 24)),
  ],
)
```

-----

### \#\# Row vs. Column: মূল পার্থক্য

সহজভাবে মনে রাখার জন্য:

  * **Row** অনেকটা একটি **ইংরেজি বাক্যের** মতো, যেখানে শব্দগুলো বাম থেকে ডানে যায়।

      * **Main Axis (মূল অক্ষ)**: Horizontal (অনুভূমিক)
      * **Cross Axis (আড়াআড়ি অক্ষ)**: Vertical (উল্লম্ব)

  * **Column** অনেকটা একটি **শপিং লিস্টের** মতো, যেখানে জিনিসগুলো একটির নিচে একটি করে লেখা থাকে।

      * **Main Axis (মূল অক্ষ)**: Vertical (উল্লম্ব)
      * **Cross Axis (আড়াআড়ি অক্ষ)**: Horizontal (অনুভূমিক)
   




Flutter-এ `style` প্রোপার্টিটি বিভিন্ন উইজেটে ব্যবহার হয়, তবে সবচেয়ে বেশি ব্যবহৃত হয় **`Text`** উইজেটের সাথে। `Text` উইজেটের `style` প্রোপার্টির ভেতরে একটি **`TextStyle`** অবজেক্ট দিতে হয়, যার মাধ্যমে আপনি লেখাটিকে নিজের ইচ্ছামতো ডিজাইন করতে পারেন।

এছাড়াও `ElevatedButton`-এর মতো উইজেটগুলোতেও `style` প্রোপার্টি থাকে, কিন্তু সেখানে `ButtonStyle` অবজেক্ট ব্যবহার করা হয়।

নিচে `TextStyle`-এর মধ্যে কী কী ব্যবহার করা যায় তার একটি তালিকা দেওয়া হলো।

-----

### \#\# ✍️ TextStyle-এর মধ্যে যা যা ব্যবহার করা যায়

#### \#\#\# মৌলিক স্টাইল

  * **`color`**: লেখার রঙ পরিবর্তন করার জন্য। (`color: Colors.red`)
  * **`fontSize`**: লেখার আকার বা সাইজ বড়/ছোট করার জন্য। (`fontSize: 24.0`)
  * **`fontWeight`**: লেখা কতটা মোটা বা চিকন হবে তা নির্ধারণ করে। (`fontWeight: FontWeight.bold`)
  * **`fontStyle`**: লেখাটিকে বাঁকা (italic) করার জন্য। (`fontStyle: FontStyle.italic`)

#### \#\#\# ফন্ট ও স্পেসিং

  * **`fontFamily`**: নির্দিষ্ট কোনো ফন্ট (যেমন: `GoogleFonts` থেকে আনা 'Roboto', 'OpenSans' ইত্যাদি) ব্যবহার করার জন্য। (`fontFamily: 'Roboto'`)
  * **`letterSpacing`**: প্রতিটি অক্ষরের মধ্যে ফাঁকা জায়গা বাড়ানোর জন্য। (`letterSpacing: 2.0`)
  * **`wordSpacing`**: প্রতিটি শব্দের মধ্যে ফাঁকা জায়গা বাড়ানোর জন্য। (`wordSpacing: 5.0`)
  * **`height`**: লাইনগুলোর মধ্যে উচ্চতা বা ফাঁকা জায়গা বাড়ানোর জন্য। (`height: 1.5`)

#### \#\#\# ডেকোরেশন

  * **`decoration`**: লেখার নিচে, উপরে বা মাঝখানে লাইন দেওয়ার জন্য।
      * `TextDecoration.underline` (নিচে লাইন)
      * `TextDecoration.overline` (উপরে লাইন)
      * `TextDecoration.lineThrough` (মাঝখানে লাইন)
  * **`decorationColor`**: ডেকোরেশন লাইনের রঙ পরিবর্তন করে।
  * **`decorationStyle`**: ডেকোরেশন লাইনের স্টাইল পরিবর্তন করে (যেমন: `dotted`, `dashed`, `wavy` ইত্যাদি)।
  * **`decorationThickness`**: ডেকোরেশন লাইনটি কতটা মোটা হবে তা নির্ধারণ করে।

#### \#\#\# অন্যান্য ইফেক্ট

  * **`backgroundColor`**: শুধুমাত্র লেখার পেছনের অংশে রঙ দেওয়ার জন্য।
  * **`shadows`**: লেখার নিচে এক বা একাধিক ছায়া (shadow) দেওয়ার জন্য।
  * **`foreground`**: লেখার রঙ হিসেবে সলিড রঙের পরিবর্তে গ্র্যাডিয়েন্ট বা অন্য কোনো ইফেক্ট দেওয়ার জন্য।

-----

### \#\# কোড উদাহরণ

নিচে উপরের কয়েকটি প্রোপার্টি ব্যবহার করে একটি সম্পূর্ণ উদাহরণ দেওয়া হলো:

```dart
import 'package:flutter/material.dart';
import 'package:google_fonts/google_fonts.dart';

class StyleExample extends StatelessWidget {
  const StyleExample({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      body: Center(
        child: Text(
          'Hello, Flutter!',
          style: TextStyle(
            // --- মৌলিক স্টাইল ---
            color: Colors.deepPurple,       // লেখার রঙ
            fontSize: 32.0,                   // ফন্টের আকার
            fontWeight: FontWeight.bold,      // লেখাটিকে বোল্ড করা হয়েছে
            fontStyle: FontStyle.italic,    // লেখাটিকে ইটালিক করা হয়েছে

            // --- ফন্ট ও স্পেসিং ---
            // fontFamily: 'Roboto',        // নির্দিষ্ট ফন্ট (GoogleFonts ছাড়া)
            letterSpacing: 1.5,               // অক্ষরগুলোর মধ্যে স্পেস

            // --- ডেকোরেশন ---
            decoration: TextDecoration.underline, // লেখার নিচে লাইন
            decorationColor: Colors.red,          // ডেকোরেশন লাইনের রঙ
            decorationStyle: TextDecorationStyle.wavy, // লাইনের স্টাইল
            decorationThickness: 2.0,

            // --- অন্যান্য ইফেক্ট ---
            backgroundColor: Colors.yellow[100], // লেখার পেছনের রঙ
            shadows: [
              Shadow(
                color: Colors.black.withOpacity(0.5),
                offset: Offset(2, 2),
                blurRadius: 3,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```
