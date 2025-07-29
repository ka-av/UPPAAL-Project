# UPPAAL-Project
ASSUMPTIONS: 
1. The transcript indicates that the scholarship application is rejected when it has not been submitted. 
2. In the transcript view, if the user wants to go back, he/she should navigate manually; otherwise, the user remains on the transcript view. 
3. It is also assumed that the Scholarship Approval Committee resides within the academic server and interacts with the portal via said server, for a simpler and more efficient template design.
4. It is also assumed that the information given by the user/student during the CGPA input is true, and no falsehoods are detected while approving/disapproving the
scholarship.
5. Assuming that one can view student/user personal information on clicking the corresponding option since we haven't learnt to display some output on UPPAAL.
   
Description: 

The model has three templates as our system namely Student, Portal and Academic server. The user actively interacts with the website in order to apply for a merit
scholarship or merit-cum-need scholarship. Conditions for a merit scholarship includes a CGPA greater than or equal to 9.0 and subsequently the merit-cum-need scholarship includes a CGPA greater than or equal to 7.0 . The model checks whether the user has enough CGPA to apply for a scholarship or not, if he has the cut off CGPA then the user gets to apply for a scholarship. First, the website asks the student to login in with his/her credentials. If the credentials are approved then the student is allowed to continue to the portal’s homepage, if rejected then they are redirected to the login page. Once the credentials are approved the student will get four options on the homepage: 
a. Apply for a scholarship 
b. Fetch academic transcript from server 
c. View personal information 
d. Log out 
When the student applies for a scholarship, he will have the two options mentioned above and the form will be approved and rejected based on the cut off CGPA. When the student clicks to view the personal information, they will be given the option to go back. In the case of “fetch academic transcript from server” the student will be given the options of viewing the transcript and going back to the homepage.  Once the user has applied for a scholarship they can no longer apply for another scholarship and after that they can only view their personal information, transcript and logout. 
Once logged out, the session will end and the model will be reset and the new student will once again have to fill the credentials to access the portal. 

Safety Properties: - 
1. Deadlock check: 
A[] not deadlock 
Explanation: checking that no deadlocks occur for all paths in the system.
 
3. Authentication Must Complete Before Moving to Home: 
A[] !(Portal.Homepage && !authsucc) 
Explanation: The portal cannot enter the Home state unless the user is authenticated.

4. No Scholarship Application After Submission: 
A[] Portal.Homepage imply !Portal.m && !Portal.mcn 
Explanation: Once a scholarship is submitted, no further application can be made in the same session.

Liveness Properties: - 
1. Transcript Fetch: 
E<> Student.Fetch_Transcript 
Explanation: Ensure that a student can eventually fetch their academic transcript.

2. Single Scholarship Application per session: 
E<> Portal.ApplyForScholarship imply Student.SignIn && !(Student.scholarship) 
Explanation: the Portal eventually reaches a state where the student applies for a scholarship, then the student must have already signed in and must not yet have a scholarship.
