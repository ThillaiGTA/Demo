<!DOCTYPE html>
<html ng-app="sapp">
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.6.9/angular.min.js"></script>
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
   <style>
		
        div{
            font:15px Verdana;
            width:450px;
        }
        table, input {
            text-align:left;
            font:13px Verdana;
        }
        table, td, th 
        {
            margin:10px 0;
            padding:2px 10px;
        }
        td, th {
            border:solid 1px #CCC;
        }
        button {
            font:13px Verdana;
            padding:3px 5px;
        }
		button {
		background-color: #4CAF50; /* Green */
		border: none;
		color: white;
		padding: 16px 32px;
		text-align: center;
		text-decoration: none;
		display: inline-block;
		font-size: 16px;
		margin: 4px 2px;
		-webkit-transition-duration: 0.4s; /* Safari */
		transition-duration: 0.4s;
		cursor: pointer;
	} 	
	#panel, #flip {
	padding: 50px;
	text-align: center;
	background-color: #e5eecc;
	border: solid 1px #c3c3c3;
}
	#panel {
	padding: 50px;
	display: none;
}
</style>
<body align="center" ng-controller="scontrol">
<div id="flip">Click to Enter details</div>
<div id="panel">
<h2>FORM</h2>
<p> Name: <input type="text" ng-model="sname"></p>
<p> Email: <input type="text" ng-model="smail"></p>
<p> Phone: <input type="Number" ng-model="snum"></p>
 <label for="gender" >Gender</label> <br />
     <select id="gender" ng-model="sgender">
        <option value="male">Male</option>
        <option value="female">Female</option>
        <option value="male">NoMention</option>
 </select></br></br>
 <button ng-click="addRow()"> ADD</button> 
 <button ng-click="removeRow()">Remove Row</button>
 <button ng-click="editRow()">Edit Row</button>
 </div>
<div id="flip1">Click to view table</div>
<div id="panel1"> 
 <table> 
            <tr>
				<th>S.NO</th>
                <th>NAME</th>
                <th>MAIL</th>
                <th>PHONE</th>
                <th>GENDER</th>
				<th>Remove</th>
				<th>Edit</th>
            </tr>
            <tr ng-repeat="student in Array">
                <td><label>{{$index + 1}}</label></td>
                <td><label>{{student.sname}}</label></td>
                <td><label>{{student.smail}}</label></td>
				<td><label>{{student.snum}}</label></td>
				<td><label>{{student.sgender}}</label></td>
                <td><input type="checkbox" ng-model="student.Remove"/></td>
				<td><input type="checkbox" ng-model="student.Edit"/></td>
            </tr>
        </table>
</div>
<script>
var app = angular.module('sapp', []);
    app.controller('scontrol', function ($scope) {
	$scope.Array =[];
        $scope.addRow = function () {
            if ($scope.sname != undefined && $scope.smail != undefined&& $scope.snum != undefined) {
                var student = [];
                student.sname = $scope.sname;
                student.smail = $scope.smail;
                student.snum = $scope.snum;
				student.sgender = $scope.sgender;
                $scope.Array.push(student);
                $scope.sname = null;
                $scope.smail = null;
                $scope.snum = null;
				$scope.sgender=null;
            }
        };
		$scope.removeRow = function () {
            var arr = [];
            angular.forEach($scope.Array, function (value) {
                if (!value.Remove) {
                    arr.push(value);
                }
            });
            $scope.Array = arr;
        };
		    $scope.submit = function () {
            var arr= [];
            angular.forEach($scope.Array, function (value) {
                arr.push('Name:' + value.sname + ', Mail:' + value.smail+ ', Number:' + value.snum+ ', Gender:' + value.sgender);
            });
            $scope.display = arr;
        };
   
	$scope.editRow = function () {
	var arr=[];
	   angular.forEach($scope.Array, function (value) {
	   if(value.Edit)
	   {
             $scope.sname=value.sname;
             $scope.smail=value.smail;
             $scope.snum=value.snum;
             $scope.sgender=value.sgender;
        }
		if (!value.Edit) {
                arr.push(value);
                }
		});
            $scope.Array = arr;
		    $scope.display = arr; 
		};
		});
</script>
<script>
$(document).ready(function(){
  $("#flip").click(function(){
    $("#panel").slideToggle("slow");
  });
});
$(document).ready(function(){
  $("#flip1").click(function(){
    $("#panel1").slideToggle("slow");
  });
});
</script>
</body>
</html>
