Previusly we are working in a student project. And all student are viewing in `resources > views > student.blade.php` file. The query code below →
```
@foreach($student as $learner)

    <tr>
        <td><a href="/student/{{$learner->id}}">{{$learner->id}}</a></td>
        <td>{{$learner->full_name}}</td>
        <td>{{$learner->age}}</td>
        <td>{{$learner->email}}</td>
        <td>{{$learner->father_name}}</td>
        <td>{{$learner->mother_name}}</td>
        <td>{{$learner->present_address}}</td>
        <td>{{$learner->permanent_address}}</td>
        <td>{{$learner->school_name}}</td>
        <td>{{$learner->phone_number}}</td>
        <td>{{$learner->date_of_birth}}</td>
        <td>{{$learner->profile_picture}}</td>
        <td>{{$learner->updated_at}}</td>
    </tr>

@endforeach
```
- So we just create links for all students `<td><a href="/student/{{$learner->id}}">{{$learner->id}}</a></td>`
- Then we need to create a single page for all students. Go to `routes > web.php` and write `Route::get('/student/{full_name}', 'App\Http\Controllers\StudentController@show');`
- We have a controller called `StudentController.php` in `app > http > contorllers` and we write some code like below
```PHP
/**
 * Display the specified resource.
 *
 * @param  \App\Models\Student  $student
 * @return \Illuminate\Http\Response
 */
public function show(Student $student, $id)
{
    // findOrFail for showing 404 when someone visit any link which is not generated via ID.
    $student = Student::findOrFail($id);
    // Passing leaner single data to single page. learner data generated from loop.
    return view('single-student', ['learner' => $student]);
}
```
- Then we need to create a view file `single-student.blade.php` for single page in `resources > views` folder and shows single data by below code
```PHP
<ul>
    <li><strong>ID: </strong>{{$learner->id}}</li>
    <li><strong>Full Name: </strong>{{$learner->full_name}}</li>
    <li><strong>Age: </strong>{{$learner->age}}</li>
    <li><strong>Email: </strong>{{$learner->email}}</li>
    <li><strong>Father Name: </strong>{{$learner->father_name}}</li>
    <li><strong>Mother Name: </strong>{{$learner->mother_name}}</li>
    <li><strong>Present Student: </strong>{{$learner->present_address}}</li>
    <li><strong>Permanent Address: </strong>{{$learner->permanent_address}}</li>
    <li><strong>School Name: </strong>{{$learner->school_name}}</li>
    <li><strong>Phone Number: </strong>{{$learner->phone_number}}</li>
    <li><strong>Date of Birth: </strong>{{$learner->date_of_birth}}</li>
    <li><strong>Profile Picture: </strong>{{$learner->profile_picture}}</li>
    <li><strong>Updated Date: </strong>{{$learner->updated_at}}</li>
</ul>

<a href="/student">Back to student list..</a>
```
