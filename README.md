# smartitude
Database files related to Smartitude

# Database Schema documentation

Generated by MySQL Workbench Model Documentation v1.0.0 - Copyright (c) 2015 Hieu Le

## Table: `user`

### Description: 

Stores the general information of each user. This is the parent table for student and faculty tables.


### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_user` | INT | PRIMARY, Not null |   | Unique identifier for each user. AUTO GENERATED |
| `email_user` | VARCHAR(255) | Not null |   | Email address of the user. |
| `password_user` | VARCHAR(32) | Not null |   | Password of the user used for login. |
| `create_time_user` | TIMESTAMP | Not null | `CURRENT_TIMESTAMP` | Timestamp of creation time of user. |
| `phone_user` | INT | Not null |   | Phone number of the user. |
| `type_user` | CHAR(1) | Not null |   | Type of the user used for login. S - Student, F - Facutly, I - Faculty In Charge |
| `name_user` | VARCHAR(45) | Not null |   | Name of the user used for login. |
| `update_time` | TIMESTAMP | Not null |   | Timestamp of last updation time of user. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_user` | PRIMARY |   |


## Table: `student`

### Description: 

Stores the general information of each student user.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_stud` | INT | PRIMARY, Not null |   | Unique identifier for each stuent. Inherited from users table.<br /><br />**foreign key** to column `id_user` on table `user`. |
| `dept_stud` | TINYINT | Not null |   | Identifier of the department to which the student belongs to.<br /><br />**foreign key** to column `id_dept` on table `department`. |
| `batch_stud` | INT | Not null |   | Batch to which the student belongs to. |
| `score_stud` | DECIMAL | Not null |   | Overall average score of a student. |
| `rank_student` | INT |  |   | Overall rank of the student among all the app users. |
| `group_stud` | INT | Not null |   | Used for classifying students based on their skills. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| id_student_idx | `id_stud` | INDEX |   |
| PRIMARY | `id_stud` | PRIMARY |   |
| id_dept_idx | `dept_stud` | INDEX |   |


## Table: `question`

### Description: 

Stores the details of each questions.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_qstn` | INT | PRIMARY, Not null |   | Unique identifier for each question. AUTO GENERATED |
| `qstn` | TEXT | Not null |   |   |
| `creator_qstn` | VARCHAR(16) | Not null |   |  **foreign key** to column `id_faculty` on table `faculty`. |
| `category_qstn` | INT | Not null |   |  **foreign key** to column `id_category` on table `category`. |
| `subcat_qstn` | INT | Not null |   |  **foreign key** to column `id_subcat` on table `subcategory`. |
| `approval_stat_qstn` | TINYINT | Not null |   |   |
| `difficulty_qstn` | INT | Not null |   |   |
| `times_attempt_qstn` | INT | Not null | `0` |   |
| `times_solved_qstn` | INT | Not null | `0` |   |
| `create_time_qstn` | TIMESTAMP |  | `CURRENT_TIMESTAMP` |   |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_qstn` | PRIMARY |   |
| id_creator_idx | `creator_qstn` | INDEX |   |
| category_qstn_idx | `category_qstn` | INDEX |   |
| subcat_qstn_idx | `subcat_qstn` | INDEX |   |


## Table: `faculty`

### Description: 

Stores the general inforation of each faculty user.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_faculty` | INT | PRIMARY, Not null |   | Unique identifier field for each faculty. Inherited from the users table.<br /><br />**foreign key** to column `id_user` on table `user`. |
| `dept_faculty` | INT | Not null |   | Department to which the faculty belongs to.<br /><br />**foreign key** to column `id_dept` on table `department`. |
| `category_faculty` | INT | Not null |   | Category assigned to the faculty to handle. The faculty can add questions to this category only.<br /><br />**foreign key** to column `id_category` on table `category`. |
| `subcat_faculty` | JSON | Not null |   | List of subcategories assigned to the faculty to handle. The faculty can add questions to these subcategories only. One faculty can have multiple subcategories. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_faculty` | PRIMARY |   |
| id_dept_idx | `dept_faculty` | INDEX |   |
| category_faculty_idx | `category_faculty` | INDEX |   |


## Table: `department`

### Description: 

Stores the details of each department.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_dept` | TINYINT | PRIMARY, Not null |   | Unique identifier for each department. AUTO GENERATED |
| `dept_name` | VARCHAR(45) | Not null |   |   |
| `dept_desc` | TEXT |  |   |   |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_dept` | PRIMARY |   |


## Table: `admin_quiz`

### Description: 

Stores the general inforation of each quiz created by admin.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_quiz_admin` | INT | Auto increments, Not null |   | Unique identifier for each quiz created by admin.<br /><br />**foreign key** to column `id_quiz` on table `quiz`. |
| `targets_quiz_admin` | INT | Not null |   | Target batch of the quiz. |
| `create_time_quiz_admin` | TIMESTAMP | Not null |   | Date and time from when the quiz is valid. |
| `expiry_time_quiz_admin` | TIMESTAMP | Not null |   | Date and time upto which the quiz is valid. |
| `id_admin` | INT | Not null |   |  **foreign key** to column `id_admin` on table `admin`. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| id_quiz_admin_idx | `id_quiz_admin` | INDEX |   |
| id_admin_idx | `id_admin` | INDEX |   |


## Table: `message`

### Description: 



### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_msg` | INT | PRIMARY, Not null |   |   |
| `title_msg` | VARCHAR(60) | Not null |   |   |
| `desc_msg` | TEXT |  |   |   |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_msg` | PRIMARY |   |


## Table: `subcategory`

### Description: 

Stores the general inforation of each question subcategory.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_subcat` | INT | PRIMARY, Auto increments, Not null |   | Unique identifier for each subcategory. |
| `id_category` | INT | Not null |   | ID of the category to which the subcategory belongs to.<br /><br />**foreign key** to column `id_category` on table `category`. |
| `icon_subcat` | TEXT |  |   | Link to the icon file related to that subcategory. |
| `name_subcat` | VARCHAR(45) | Not null |   | Name of the subcategory. |
| `desc_subcat` | VARCHAR(45) |  |   | Short description of the subcategory. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_subcat` | PRIMARY |   |
| id_category_idx | `id_category` | INDEX |   |


## Table: `category`

### Description: 

Stores the general inforation of each question category.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_category` | INT | PRIMARY, Not null |   | Unique identifier for each category. AUTO GENERATED |
| `name_category` | VARCHAR(45) | Not null |   | Name of the category. |
| `desc_category` | TEXT |  |   | Short description of the category. |
| `icon_category` | TEXT |  |   | Link to the icon file related to that category. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_category` | PRIMARY |   |


## Table: `faculty_in_charge`

### Description: 

Stores the general inforation of each faculty in-charge user.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_faculty_in_charge` | INT | PRIMARY, Not null |   | Unique identifier field for each faculty in-charge. Inherited from the faculty table which inherits it from users table.<br /><br />**foreign key** to column `id_faculty` on table `faculty`. |
| `in_charge_subcat` | JSON | Not null |   | List of subcategories assigned to the faculty in-charge to handle. The faculty can approve or reject questions of these subcategories only. One faculty in-charge can have multiple subcategory associations. JSON file contains list of subcategory IDs. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_faculty_in_charge` | PRIMARY |   |


## Table: `admin`

### Description: 

Stores the general information of each admin user.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_admin` | INT | PRIMARY, Not null |   | Unique identifier for each row in admin table. AUTO GENERATED |
| `username` | VARCHAR(16) | Not null, Unique |   | Name of the admin user used for login. |
| `email` | VARCHAR(255) | Not null |   | Email address of the admin user. |
| `password` | VARCHAR(32) | Not null |   | Password of the admin user used for login. |
| `create_time` | TIMESTAMP |  | `CURRENT_TIMESTAMP` | Timestamp of creation time of admin user. |
| `update_time` | TIMESTAMP |  |   | Timestamp of last updation time of admin user. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_admin` | PRIMARY |   |
| username_UNIQUE | `username` | UNIQUE |   |


## Table: `student_quiz`

### Description: 

Stores the general inforation of each quiz created by student.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_quiz_stud` | INT | Auto increments, Not null |   | Unique identifier for each quiz created by admin.<br /><br />**foreign key** to column `id_quiz` on table `quiz`. |
| `create_time_quiz_stud` | TIMESTAMP | Not null | `CURRENT_TIMESTAMP` | Date and time from when the quiz is created. |
| `id_student` | INT | Not null |   |  **foreign key** to column `id_stud` on table `student`. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| id_quiz_stud_idx | `id_quiz_stud` | INDEX |   |
| id_student_idx | `id_student` | INDEX |   |


## Table: `quiz`

### Description: 

Stores the general inforation of each quiz that is common for the quizzes created by either the admin or the student.

### Columns: 

| Column | Data type | Attributes | Default | Description |
| --- | --- | --- | --- | ---  |
| `id_quiz` | INT | PRIMARY, Auto increments, Not null |   | Unique identifier for each quiz created by admin. |
| `targets_quiz` | INT | Not null |   | Target batch of the quiz. |
| `create_time_quiz` | DATETIME | Not null |   | Date and time from when the quiz is valid. |
| `desc_quiz` | TEXT | Not null |   | Short description of the quiz. |
| `section_times` | JSON | Not null |   | Time allotted for each section. JSON file containing category ID and time allotted for each category. |


### Indices: 

| Name | Columns | Type | Description |
| --- | --- | --- | --- |
| PRIMARY | `id_quiz` | PRIMARY |   |