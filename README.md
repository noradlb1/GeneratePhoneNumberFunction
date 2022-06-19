    Private r As New Random
    Private Function GeneratePhoneNumber() As String
        Dim npa, nxx, xxxx As String
        Dim reg As Regex = New Regex("^([2-9][0-8]\d)$")
        Do
            npa = r.Next(100, 1000).ToString()
        Loop Until reg.IsMatch(npa)

        reg = New Regex("[2-9]((0|[2-9])\d|\d(0|[2-9]))")
        Do
            nxx = r.Next(100, 1000).ToString()
        Loop Until reg.IsMatch(nxx)

        xxxx = r.Next(1000, 10000).ToString()
        Return If((npa = "800" AndAlso nxx = "555") OrElse (nxx = "555" AndAlso xxxx = "0128"), GeneratePhoneNumber, String.Join("-", {npa, nxx, xxxx}))
    End Function

    Private Sub Button1_Click(sender As Object, e As EventArgs) Handles Button1.Click
        TextBox1.Text = r.Next

    End Sub
