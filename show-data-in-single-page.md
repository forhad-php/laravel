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
- Now we need to create a single page for all students. Go to `routes > web.php` and write `Route::get('/student/{full_name}', 'App\Http\Controllers\StudentController@show');`
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
