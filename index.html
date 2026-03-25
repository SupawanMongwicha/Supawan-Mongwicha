using System;
using System.Configuration;
using System.Data;
using System.IO;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Web.Security;
using System.Web.UI;
using System.Web.UI.WebControls;
using System.Data.SqlClient;
using DMWtest.Class;
using System.Globalization;
using System.Data.SqlTypes;
using System.Xml.Linq;

namespace DMWtest.External
{
    public partial class ExternalSubmission : System.Web.UI.Page
    {
        readonly Class.DatabaseClass dbClass = new Class.DatabaseClass();
        readonly Class.ReusableClass RClass = new Class.ReusableClass();
        readonly Document.Response ResponseClass = new Document.Response();
        readonly string folderPath = ConfigurationManager.AppSettings["Location"];

        DataTable dt;
        string query, values;
        readonly string SPName = "SAM_DMW_QA_SP @value0, @value1";
        protected void Page_Load(object sender, EventArgs e)
        {
            CheckBox2.Visible = false;
            if (!this.Page.User.Identity.IsAuthenticated)
            {
                FormsAuthentication.RedirectToLoginPage();
            }
            if (!IsPostBack)
            {
                ChkWorkflow.Checked = false;
                string uniqueID = Guid.NewGuid().ToString();
                LblGuid.Text = uniqueID;
                LblTransnum.Text = "";
                BindDLL();
                // LoadRequester();
                // GetPrevRevision();
                //  Status.Text = "Open";
                if (!string.IsNullOrWhiteSpace(Request.QueryString["ID"]))
                {
                    LoadIncident(Request.QueryString["ID"].ToString());
                    DisableForUpdate();
                    ChangeActivity();

                    ForceEnableSubmitOnlyForRejectedOwner();

                }
                GetDroNo();
                if (DDLDoctype.SelectedValue == "")
                {
                    BtnSubmit.Enabled = false;
                }
                
            }

        }

        protected void LoadIncident(string TransNum)
        {
            BtnUser1Submit.Enabled = false;
            query = "SELECT Document_Type, CIBNo,DRONo, Customer,DocumentDesc, CIBRevision,DocUploadUser, USERRevision, Effective_Date,Status, Initiator, Requester, Comment, Concurrent_Approval FROM SAM_DMW_ExternalForm WHERE Trans_Num = @value0";
            dt = dbClass.LoadData(query, TransNum);
            if (dt.Rows.Count > 0)
            {
                DDLDoctype.SelectedValue = dt.Rows[0]["Document_Type"].ToString();
                txtCIBNumber.Text = dt.Rows[0]["CIBNo"].ToString();
                DDLCustomer.SelectedValue = dt.Rows[0]["Customer"].ToString();
                TxtRevision.Text = dt.Rows[0]["CIBRevision"].ToString();
                Revision.Text = dt.Rows[0]["USERRevision"].ToString();
                TxtEffectiveDate.Text = Convert.ToDateTime(dt.Rows[0]["Effective_Date"]).ToString("yyyy-MM-dd");
                //DDlStatus.SelectedValue= dt.Rows[0]["Status"].ToString();
                lblDRONo.Text = dt.Rows[0]["DRONo"].ToString();
                TxtComment.Text = dt.Rows[0]["Comment"].ToString();
                txtDocumentDesc.Text = dt.Rows[0]["DocumentDesc"].ToString();
                DDLRequester.SelectedValue = dt.Rows[0]["Requester"].ToString();
                DDLUploadUser.SelectedValue = dt.Rows[0]["DocUploadUser"].ToString();
                //CheckBox2.Checked = bool.Parse(dt.Rows[0]["Concurrent_Approval"].ToString());
                BindGVFileUpload(folderPath + TransNum);
                if (dt.Rows[0]["DocUploadUser"].ToString() == User.Identity.Name.ToString())
                {
                    BtnSubmit.Enabled = true;
                    BtnUser1Submit.Enabled = true;
                }
                else
                {
                    BtnSubmit.Enabled = false;
                    BtnUser1Submit.Enabled = false;
                }
                //
                // Ensure Status label reflects DB value, then determine UI behavior
                string status = (dt.Rows[0]["Status"] ?? "").ToString().Trim();
                Status.Text = status;

                bool isRejected = status.Equals("Rejected", StringComparison.OrdinalIgnoreCase)
                               || status.Equals("Reject", StringComparison.OrdinalIgnoreCase);

                // only the Requester (person who requested the change) can perform Resubmit
                bool isRequester = (dt.Rows[0]["Requester"] ?? "").ToString().Equals(User.Identity.Name, StringComparison.OrdinalIgnoreCase);

                // Only the Requester can Resubmit a rejected item
                BtnResubmit.Visible = isRejected && isRequester;

                if (isRejected)
                {
                    BtnSubmit.Visible = false;  
                }

                // If the record is Open (including after Resubmit), lock requester fields so they cannot edit again
                if (status.Equals("Open", StringComparison.OrdinalIgnoreCase) && isRequester)
                {
                    Disable(); // disables main inputs and submit/update buttons for requester
                    BtnResubmit.Visible = false;
                    BtnUser1Submit.Enabled = false; // ensure user-level submit also disabled
                }

                //


            }
            else
            {
                LblMessage.Text = "Error: No Records Found";
            }
        }
        //protected void LoadRequester()
        //{
        //    DateTime CurrentDate = DateTime.Now;
        //    TxtEffectiveDate.Text = CurrentDate.ToString("yyyy/MM/dd");

        //    string DocType = DDLDoctype.SelectedValue.ToString();
        //    //RClass.BindDDL(DDLProgram, SPName, "Category_Program|" + DDLDoctype.SelectedValue.Replace(" ", "") + "");
        //    //string DocType = DDLDoctype.SelectedValue;
        //    string username = User.Identity.Name.ToString();
        //    string Requester_query = "select L1_Approver_ID,L2_Approver_ID,L3_Approver_ID,L4_Approver_ID,L5_Approver_ID from SAM_DMW_WorkFlow where Document_Type= @value0";
        //    if (DocType.ToString() != "")
        //    {
        //        DataTable Requester_dt = dbClass.LoadData(Requester_query, DocType.ToString());


        //    if (Requester_dt.Rows.Count > 0)
        //    {
        //        if ((!string.IsNullOrWhiteSpace(Requester_dt.Rows[0]["L1_Approver_ID"].ToString())))
        //        {
        //            if (Requester_dt.Rows[0]["L1_Approver_ID"].ToString() == username.ToString().Substring(username.ToString().Length - 7, 7))
        //            {
        //                DDLRequester.Items.Remove(DDLRequester.Items.FindByValue(Requester_dt.Rows[0]["L1_Approver_ID"].ToString()));
        //            }

        //        }
        //        if ((!string.IsNullOrWhiteSpace(Requester_dt.Rows[0]["L2_Approver_ID"].ToString())))
        //        {
        //            if (Requester_dt.Rows[0]["L1_Approver_ID"].ToString() == username.ToString().Substring(username.ToString().Length - 7, 7))
        //            {
        //                DDLRequester.Items.Remove(DDLRequester.Items.FindByValue(Requester_dt.Rows[0]["L2_Approver_ID"].ToString()));
        //            }

        //        }
        //        if ((!string.IsNullOrWhiteSpace(Requester_dt.Rows[0]["L3_Approver_ID"].ToString())))
        //        {
        //            if (Requester_dt.Rows[0]["L1_Approver_ID"].ToString() == username.ToString().Substring(username.ToString().Length - 7, 7))
        //            {
        //                DDLRequester.Items.Remove(DDLRequester.Items.FindByValue(Requester_dt.Rows[0]["L3_Approver_ID"].ToString()));
        //            }

        //        }
        //        if ((!string.IsNullOrWhiteSpace(Requester_dt.Rows[0]["L4_Approver_ID"].ToString())))
        //        {
        //            if (Requester_dt.Rows[0]["L1_Approver_ID"].ToString() == username.ToString().Substring(username.ToString().Length - 7, 7))
        //            {
        //                DDLRequester.Items.Remove(DDLRequester.Items.FindByValue(Requester_dt.Rows[0]["L4_Approver_ID"].ToString()));
        //            }

        //        }
        //        if ((!string.IsNullOrWhiteSpace(Requester_dt.Rows[0]["L5_Approver_ID"].ToString())))
        //        {
        //            if (Requester_dt.Rows[0]["L1_Approver_ID"].ToString() == username.ToString().Substring(username.ToString().Length - 7, 7))
        //            {
        //                DDLRequester.Items.Remove(DDLRequester.Items.FindByValue(Requester_dt.Rows[0]["L5_Approver_ID"].ToString()));
        //            }

        //        }
        //    }
        //}

        //}

        protected void BindDLL()
        {

            RClass.BindDDL(DDLDoctype, SPName, "ExternalDocType|");
            RClass.BindDDL(DDLCustomer, SPName, "Customer|");
            RClass.BindDDL(DDLRequester, SPName, "Requester|");
            RClass.BindDDL(DDLUploadUser, SPName, "Requester|");
            //ExternalPanel
            RClass.BindDDL(DDLENGName1, SPName, "Requester|");
            RClass.BindDDL(DDLENGName2, SPName, "Requester|");
            RClass.BindDDL(DDLENGName3, SPName, "Requester|");
            //   RClass.BindDDL(DDLENGName4, SPName, "Requester|");
            //  RClass.BindDDL(DDLENGName5, SPName, "Requester|");
            // RClass.BindDDL(DDLENGName6, SPName, "Requester|");
            // RClass.BindDDL(DDLENGName7, SPName, "Requester|");
            // RClass.BindDDL(DDLENGName8, SPName, "Requester|");
            // RClass.BindDDL(DDLENGName9, SPName, "Requester|");
            // RClass.BindDDL(DDLENGName10, SPName, "Requester|");
            RClass.BindDDL(DDLQAName1, SPName, "Requester|");
            RClass.BindDDL(DDLQAName2, SPName, "Requester|");
            RClass.BindDDL(DDLQAName3, SPName, "Requester|");
            //RClass.BindDDL(DDLQAName4, SPName, "Requester|");
            //RClass.BindDDL(DDLQAName5, SPName, "Requester|");
            //RClass.BindDDL(DDLQAName6, SPName, "Requester|");
            //RClass.BindDDL(DDLQAName7, SPName, "Requester|");
            //RClass.BindDDL(DDLQAName8, SPName, "Requester|");
            //RClass.BindDDL(DDLQAName9, SPName, "Requester|");
            //RClass.BindDDL(DDLQAName10, SPName, "Requester|");
            RClass.BindDDL(DDLNDTName1, SPName, "Requester|");
            RClass.BindDDL(DDLNDTName2, SPName, "Requester|");
            RClass.BindDDL(DDLNDTName3, SPName, "Requester|");
            RClass.BindDDL(DDLNDTName4, SPName, "Requester|");
            RClass.BindDDL(DDLSPName1, SPName, "Requester|");
            RClass.BindDDL(DDLSPName2, SPName, "Requester|");
            RClass.BindDDL(DDLSPName3, SPName, "Requester|");
            RClass.BindDDL(DDLSCMName1, SPName, "Requester|");
            RClass.BindDDL(DDLSCMName2, SPName, "Requester|");
            RClass.BindDDL(DDLPlannerName1, SPName, "Requester|");
            RClass.BindDDL(DDLPlannerName2, SPName, "Requester|");
            RClass.BindDDL(DDLMCLName1, SPName, "Requester|");
            RClass.BindDDL(DDLMCLName2, SPName, "Requester|");
            RClass.BindDDL(DDLMCLName3, SPName, "Requester|");
            // RClass.BindDDL(DDLMCLName4, SPName, "Requester|");
            RClass.BindDDL(DDLDocControlName1, SPName, "Requester|");
            RClass.BindDDL(DDLProgramLeaderName1, SPName, "Requester|");
            RClass.BindDDL(DDLProgramLeaderName2, SPName, "Requester|");
            RClass.BindDDL(DDLProgramLeaderName3, SPName, "Requester|");
            RClass.BindDDL(DDLProgramLeaderName4, SPName, "Requester|");
            RClass.BindDDL(DDLQAMName1, SPName, "Requester|");
            //    BindCIBDDL();
            GetPrevRevision();
            DefalutName();
        }
        protected void DefalutName()
        {
            query = "select * from UserDefinedTypeValues where TypeName='SAM_DMW_CIB_Department' order by cast( Description as int )asc";
            dt = dbClass.LoadData(query, "");
            if (dt.Rows.Count > 0)
            {
                DDLENGName1.SelectedValue = dt.Rows[0]["Value"].ToString();
                //DDLENGName1.Enabled = false;
                DDLQAName1.SelectedValue = dt.Rows[1]["Value"].ToString();
                // DDLQAName1.Enabled = false;
                DDLNDTName1.SelectedValue = dt.Rows[2]["Value"].ToString();
                // DDLNDTName1.Enabled = false;
                DDLSPName1.SelectedValue = dt.Rows[3]["Value"].ToString();
                // DDLSPName1.Enabled = false;
                DDLSCMName1.SelectedValue = dt.Rows[4]["Value"].ToString();
                // DDLSCMName1.Enabled = false;
                DDLPlannerName1.SelectedValue = dt.Rows[5]["Value"].ToString();
                //DDLPlannerName1.Enabled = false;
                DDLMCLName1.SelectedValue = dt.Rows[6]["Value"].ToString();
                // DDLMCLName1.Enabled = false;
                DDLDocControlName1.SelectedValue = dt.Rows[7]["Value"].ToString();
                // DDLDocControlName1.Enabled = false;
                DDLProgramLeaderName1.SelectedValue = dt.Rows[8]["Value"].ToString();
                // DDLProgramLeaderName1.Enabled = false;
                DDLQAMName1.SelectedValue = dt.Rows[9]["Value"].ToString();
                // DDLQAMName1.Enabled = false;

            }

            //DDLENGName1.SelectedValue = "66682507";
            //DDLENGName1.Enabled = false;
            //DDLQAName1.SelectedValue = "66682507";
            //DDLQAName1.Enabled = false;
            //DDLNDTName1.SelectedValue = "66682507";
            //DDLNDTName1.Enabled = false;
            //DDLSPName1.SelectedValue = "66682507";
            //DDLSPName1.Enabled = false;
            //DDLSCMName1.SelectedValue = "66682507";
            //DDLSCMName1.Enabled = false;
            //DDLPlannerName1.SelectedValue = "66682507";
            //DDLPlannerName1.Enabled = false;
            //DDLMCLName1.SelectedValue = "66682507";
            //DDLMCLName1.Enabled = false;
            //DDLDocControlName1.SelectedValue = "66682507";
            //DDLDocControlName1.Enabled = false;
            //DDLProgramLeaderName1.SelectedValue = "66682507";
            //DDLProgramLeaderName1.Enabled = false;
            //DDLQAMName1.SelectedValue = "66682507";
            //DDLQAMName1.Enabled = false;
        }
        protected void BindCIBDDL()
        {
            for (int i = 10; i >= 0; i--)
            {
                if (i == 0)
                {
                    //DDLName.Items.Insert(0, new ListItem("Please Select", ""));
                    //  DDLComments.Items.Insert(0, new ListItem("Please Select", ""));
                    //  DDLAction.Items.Insert(0, new ListItem("Please Select", ""));
                    // DDLDate.Items.Insert(0, new ListItem("Please Select", ""));
                }
                else
                {
                    //  DDLName.Items.Insert(0, new ListItem("Name " + i, "Name " + i));
                    //  DDLComments.Items.Insert(0, new ListItem("Comments " + i, "Comments " + i));
                    //   DDLAction.Items.Insert(0, new ListItem("ActionRequired " + i, "ActionRequired " + i));
                    ///DDLDate.Items.Insert(0, new ListItem("Date " + i, "Date " + i));
                }

            }

        }
        protected void ChangeActivity()
        {

        }

        protected void GetPrevRevision()
        {
            string PrevRevision_query = "select CIBRevision,Status from SAM_DMW_ExternalForm where Delete_Record is null and Document_Type='" + DDLDoctype.SelectedValue.ToString() + "' and Customer='" + DDLCustomer.SelectedValue.ToString() + "' and CIBNo='" + txtCIBNumber.Text.ToString() + "' order by CIBRevision desc";
            // string PrevRevision_query = "select Revision from SAM_DMW_QAForm where Delete_Record is null and Document_Type='" + DDLDoctype.SelectedValue.ToString() + "' and Program='" + DDLProgram.SelectedValue.ToString() + "'  order by Revision desc";
            DataTable Requester_dt = dbClass.LoadData(PrevRevision_query, "");
            if (Requester_dt.Rows.Count > 0)
            {

                query = "SELECT COUNT(1) FROM SAM_DMW_ExternalForm WHERE Document_Type = '" + DDLDoctype.SelectedValue.ToString() + "'  AND " +
        "Status='Pending Approval' and Delete_Record is null and Customer='" + DDLCustomer.SelectedValue.ToString() + "' and CIBNo='" + txtCIBNumber.Text.ToString() + "'";
                //values = DDLDoctype.SelectedValue + "|" + DDLProgram.SelectedValue + "|" + DDLPartNo.SelectedValue + "|" + DDLOperNo.SelectedValue + "|" + Revision.Text + "|" + TxtEffectiveDate.Text + "|"
                if (dbClass.CheckExists(query, ""))
                {
                    ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Unclosed Transaction. Please close Pending request.')", true);
                    return;
                }
                else
                {
                    int getNextRevisonNum1 = Convert.ToInt32(Requester_dt.Rows[0]["CIBRevision"].ToString()) + 1;
                    // int getNextRevisonNum = Convert.ToInt32(Requester_dt.Rows[0]["Revision"].ToString().Remove(0, 1));
                    string RevionText = getNextRevisonNum1.ToString().PadLeft(2, '0');
                    TxtRevision.Text = RevionText.ToString();
                }




            }
            else
            {
                TxtRevision.Text = "01";

            }

        }
        protected void BtnUploadFile_Click(object sender, EventArgs e)
        {

            //UploadFiles upFiles = new UploadFiles();

            if (FileUpload1.HasFile)
            {


                foreach (HttpPostedFile uploadedFile in FileUpload1.PostedFiles)
                {
                    // HttpPostedFile postedFile = FileUpload1.PostedFile;

                    string filepath = Path.GetFileName(uploadedFile.FileName);
                    if (!Directory.Exists(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/")))
                    {
                        try
                        {

                            Directory.CreateDirectory(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));

                        }
                        catch (Exception ex)
                        {
                            //  CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [errorcretaepath-FileUpload1.HasFiles] Error: " + ex.Message);
                        }
                    }
                    uploadedFile.SaveAs(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/") + filepath);
                    //FilesName += uploadedFile.FileName + "<br>";

                }
                //string FilesName = "";

                ////FilesName += listofuploadedfiles.Text;
                //string[] files = Directory.GetFiles(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));

                //foreach (string file in files)
                //{
                //    FilesName += (Path.GetFileName(file)) + "<br>";
                //}
                BindGVFileUpload(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));
                //listofuploadedfiles.Text = FilesName.ToString();

            }
            else
            {
                ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('No files uploaded.')", true);
            }


        }
        protected void BtnClearFile_Click(object sender, EventArgs e)
        {
            try
            {
                var dir = new DirectoryInfo(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));
                foreach (FileInfo file in dir.EnumerateFiles())
                {
                    file.Delete();
                }
                dir.Delete();
                //listofuploadedfiles.Text = "";
                GVAttachment.DataSource = null;
                GVAttachment.DataBind();
            }
            catch (Exception ex)
            {
                ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('" + ex.Message + "')", true);
            }

        }

        protected void GetDroNo()
        {

            string _getDroQuery = "select count(Document_type) from [dbo].[SAM_DMW_ExternalForm] ";
            DataTable dtDroCount = dbClass.LoadData(_getDroQuery, "");
            int _getDrocount = 1;
            if (dtDroCount.Rows.Count > 0)
            {
                _getDrocount = Convert.ToInt32(dtDroCount.Rows[0][0].ToString()) + 1;
            }
            //txtDocumentNumber.Text= "SPTA-CIB-"+ Convert.ToString(_getDrocount).PadLeft(4, '0').ToString();
            lblDRONo.Text = (DateTime.Now.ToString("yy") + Convert.ToString(_getDrocount).PadLeft(5, '0')).ToString();
        }
        protected void BtnDocUserSubmit_Click(object sender, EventArgs e)
        {
            string constr = ConfigurationManager.ConnectionStrings["ConnStringDbLive"].ConnectionString;
            LblMessage.Text = "";
            string messageVal = "";
            int Workflow = 0;
            if (ChkWorkflow.Checked == true)
            {
                Workflow = 1;


                
                    
                    
                    
            }
            else
            {
                Workflow = 0;
            }
            query = "SELECT COUNT(1) FROM SAM_DMW_ExternalForm WHERE Document_Type = @value0 and Customer='" + DDLCustomer.SelectedValue.ToString() + "' and CIBNo='" + txtCIBNumber.Text.ToString() + "' and CIBRevision='" + TxtRevision.Text.ToString() + "' AND Delete_Record is null";
            values = DDLDoctype.SelectedValue + "|" + DDLCustomer.SelectedValue.ToString() + "|";
            if (!dbClass.CheckExists(query, values))
            {
                try
                {
                    GetDroNo();
                    string TempDate = DateTime.Now.ToString("ddMMyyyyHHmmssffffff");
                    string Depth = "0";

                    try
                    {

                        using (SqlConnection con = new SqlConnection(constr))
                        {
                            using (SqlCommand cmd = new SqlCommand("SAM_DMW_External_DocUser_Document_SP", con))
                            {
                                cmd.CommandType = CommandType.StoredProcedure;
                                con.Open();



                                cmd.Parameters.AddWithValue("@value0", DDLDoctype.SelectedValue.ToString());
                                cmd.Parameters.AddWithValue("@value1", Revision.Text.ToString());
                                cmd.Parameters.AddWithValue("@value2", TxtEffectiveDate.Text.ToString());
                                // cmd.Parameters.AddWithValue("@value3", "");
                                cmd.Parameters.AddWithValue("@value3", DDLRequester.SelectedValue.ToString());
                                cmd.Parameters.AddWithValue("@value4", DDLUploadUser.SelectedValue.ToString()); 
                                cmd.Parameters.AddWithValue("@value5", txtCIBNumber.Text.ToString());
                                cmd.Parameters.AddWithValue("@value6", txtDocumentDesc.Text.ToString());
                                cmd.Parameters.AddWithValue("@value7", lblDRONo.Text.ToString());
                                cmd.Parameters.AddWithValue("@value8", TxtComment.Text.ToString());
                                cmd.Parameters.AddWithValue("@value9", TxtRevision.Text.ToString());
                                cmd.Parameters.AddWithValue("@value10", txtRevisionDesc.Text.ToString());
                                cmd.Parameters.AddWithValue("@value11", User.Identity.Name.ToString());
                                cmd.Parameters.AddWithValue("@value12", "Submit");
                                cmd.Parameters.AddWithValue("@value13", DDLCustomer.SelectedValue.ToString());
                                cmd.Parameters.AddWithValue("@value14", "Open");
                                cmd.Parameters.AddWithValue("@value15", Workflow); //CIB Workflow for old doc
                                cmd.Parameters.AddWithValue("@value16", User.Identity.Name.ToString() + TempDate.ToString());

                                cmd.Parameters.Add("@Infobar", SqlDbType.VarChar, 1000);
                                cmd.Parameters["@Infobar"].Direction = ParameterDirection.Output;
                                cmd.Parameters.Add("@TransNum", SqlDbType.VarChar, 1000);
                                cmd.Parameters["@TransNum"].Direction = ParameterDirection.Output;
                                try
                                {


                                    cmd.ExecuteNonQuery();
                                    //BindOtherActivity();

                                    string msg = "";
                                    string Trans_Num = "";

                                    Trans_Num = cmd.Parameters["@TransNum"].Value.ToString();

                                    if (dt.Rows[0]["DocUploadUser"].ToString() == User.Identity.Name.ToString())
                                    {
                                        BtnSubmit.Enabled = true;
                                    }

                                    if (Trans_Num == "0")
                                    {
                                        ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Cannot Create Trans_num Plaese contact administrator.')", true);
                                        return;
                                    }

                                    if (cmd.Parameters["@Infobar"].Value != null)
                                    {


                                        try
                                        {

                                            string root = Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/");
                                            if (Directory.Exists(root))
                                            {
                                                string[] files = Directory.GetFiles(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));


                                                //if (FileUpload1.HasFiles)
                                                if (files.Length > 0)
                                                {

                                                    //string queryTrans_Num = "SELECT TOP 1 * FROM SAM_DMW_ExternalForm ORDER BY Trans_ID DESC";

                                                    //SqlConnection conn1 = new SqlConnection(constr);
                                                    //SqlCommand cmd1 = new SqlCommand(queryTrans_Num, conn1);
                                                    //conn1.Open();
                                                    //SqlDataReader dr1 = cmd1.ExecuteReader();
                                                    //while (dr1.Read())
                                                    //{
                                                    //    Trans_Num = dr1["Trans_Num"].ToString();
                                                    //}
                                                    //dr1.Close();
                                                    //conn1.Close();
                                                    if (!Directory.Exists(folderPath + Trans_Num))
                                                    {
                                                        try
                                                        {
                                                            string userName = Environment.UserName;
                                                            //  CommonClass.writeLog(DateTime.Now.ToString() + "- " + userName + " - [beforecreate-FileUpload1.HasFiles] Error: " + folderPath + Trans_Num);
                                                            RClass.debug("Directory not exist: create path '" + folderPath + Trans_Num + "'");
                                                            Directory.CreateDirectory(folderPath + Trans_Num);
                                                            // CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [aftercretae-FileUpload1.HasFiles] Error: " + folderPath + Trans_Num);

                                                        }
                                                        catch (Exception ex)
                                                        {
                                                            //  CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [errorcretaepath-FileUpload1.HasFiles] Error: " + ex.Message);
                                                        }
                                                    }


                                                    // foreach (HttpPostedFile uploadedFile in FileUpload1.PostedFiles)
                                                    foreach (string file in files)
                                                    {
                                                        try
                                                        {
                                                            System.IO.File.Copy(file, folderPath + Trans_Num + "//" + Path.GetFileName(file));

                                                        }
                                                        catch (Exception ex)
                                                        {
                                                            // CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [save fileupload-FileUpload1.HasFiles] Error: " + ex.Message);
                                                        }

                                                    }

                                                    var dir = new DirectoryInfo(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));
                                                    foreach (FileInfo file in dir.EnumerateFiles())
                                                    {
                                                        file.Delete();
                                                    }
                                                    dir.Delete();
                                                }
                                            }
                                            msg = cmd.Parameters["@Infobar"].Value.ToString();


                                            if (msg != "Cannot Save Data." || msg != null)
                                            {
                                                Disable();
                                                messageVal = "Successfully Submitted!";
                                                if (Workflow == 0)
                                                {
                                                    LblTransnum.Text = Trans_Num;

                                                    BtnSubmit_Click(sender, e);
                                                    if (DDLDoctype.SelectedValue == "")
                                                    {
                                                        BtnSubmit.Enabled = true;
                                                    }

                                                }
                                            }
                                            if (Workflow == 1)
                                            {
                                                LblTransnum.Text = Trans_Num;

                                                BtnSubmit_Click(sender, e);
                                                if (DDLDoctype.SelectedValue != "")
                                                {
                                                    BtnSubmit.Enabled = true;
                                                }

                                            }


                                        }
                                        catch (Exception ex)
                                        {
                                            // CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [failed  catch fileupload-FileUpload1.HasFiles] Error: " + ex.Message);
                                            RClass.insertAppExceptionLog(ex.Message.ToString(), User.Identity.Name);
                                            ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Data inserted successffuly in the database, but the file was not saved. Please contact the Administrator!.')", true);
                                            BtnUser1Submit.Enabled = false;
                                        }
                                        ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('" + messageVal + "')", true);
                                    }
                                    else
                                    {
                                        ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Cannot Create Trans_num Plaese contact administrator.')", true);
                                        //ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Data Cannot be insert')", true);
                                    }
                                }
                                catch (Exception ex)
                                {
                                    con.Close();
                                    ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('" + ex.Message + "')", true);
                                }

                            }
                        }
                    }
                    catch (Exception ex)
                    {


                    }


                }
                catch (Exception ex)
                {
                    LblMessage.Text = "Error while saving data." + ex.ToString();
                    RClass.insertAppExceptionLog(ex.ToString(), User.Identity.Name.ToString());
                }
            }
            else
            {
                if (string.IsNullOrWhiteSpace(LblMessage.Text))
                {
                    messageVal = "There is an Un-Closed transaction for this Request!";
                }
                LblMessage.Text = messageVal;
            }

            ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('" + messageVal + "')", true);
        }
        protected void BtnSubmit_Click(object sender, EventArgs e)
        {
            string Trans_num = "";
            if (LblTransnum.Text == "")
            //if(ChkWorkflow.Checked==false)
            {
                Trans_num = Request.QueryString["ID"].ToString();

            }
            else
            {
                Trans_num = LblTransnum.Text;
            }
            if (Trans_num == "")
            {
                ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Cannot Create Trans_num Plaese contact administrator.')", true);
                return;
            }
            string constr = ConfigurationManager.ConnectionStrings["ConnStringDbLive"].ConnectionString;
            LblMessage.Text = "";
            string messageVal = "";
            // Only insert ExternalType rows when none exist for this Trans_num.
            query = "SELECT COUNT(1) FROM SAM_DMW_EXTERNALTYPE WHERE Trans_num = @value0";
            //values = DDLDoctype.SelectedValue + "|"+DDLCustomer.SelectedValue.ToString()+"|";
            if (!dbClass.CheckExists(query, Trans_num))
            {
                try
                {

                    string TempDate = DateTime.Now.ToString("ddMMyyyyHHmmssffffff");
                    string Depth = "0";
                    DataTable dtExternalType = new DataTable();

                    dtExternalType = dbClass.Externaltable(dtExternalType);

                    for (int l = 1; l <= 6; l++)
                    {
                        string col = "DueDate" + l;
                        if (dtExternalType.Columns.Contains(col))
                            dtExternalType.Columns[col].DataType = typeof(DateTime);
                    }


                    //  List<ExternalDoc> externalList = new List<ExternalDoc>();
                    string ENGCurrentApprover = "";
                    string QACurrentApprover = "";
                    string NDTCurrentApprover = "";
                    string SPCPROCurrentApprover = "";
                    string PURCurrentApprover = "";
                    string PLANNERCurrentApprover = "";
                    string MCLCurrentApprover = "";
                    string DOCCONTROLCurrentApprover = "";
                    string PROGRAMCONTROLCurrentApprover = "";
                    string QAMCurrentApprover = "";
                    for (int i = 1; i <= 10; i++)
                    {
                        DataRow dr = dtExternalType.NewRow();
                        string IndexDDLName = "";
                        string IndexTXTName = "";
                        string IndexCHKName = "";
                        ExternalDoc external = new ExternalDoc();
                        external.Temp_ID = User.Identity.Name.ToString() + TempDate;
                        dr["Temp_ID"] = User.Identity.Name.ToString() + TempDate.ToString();
                        dr["Trans_ID"] = 1;
                        if (i == 1)
                        {
                            external.CIBType = "Engineering";
                            IndexDDLName = "DDLENG";
                            IndexTXTName = "TXTENG";
                            IndexCHKName = "CHKENG";
                        }
                        if (i == 2)
                        {
                            external.CIBType = "QA";
                            IndexDDLName = "DDLQA";
                            IndexTXTName = "TXTQA";
                            IndexCHKName = "CHKQA";
                        }
                        if (i == 3)
                        {
                            external.CIBType = "NDT";
                            IndexDDLName = "DDLNDT";
                            IndexTXTName = "TXTNDT";
                            IndexCHKName = "CHKNDT";
                        }
                        if (i == 4)
                        {
                            external.CIBType = "SpecialProcess";
                            IndexDDLName = "DDLSP";
                            IndexTXTName = "TXTSP";
                            IndexCHKName = "CHKSP";
                        }
                        if (i == 5)
                        {
                            external.CIBType = "Purchasing";
                            IndexDDLName = "DDLSCM";
                            IndexTXTName = "TXTSCM";
                            IndexCHKName = "CHKSCM";
                        }
                        if (i == 6)
                        {
                            external.CIBType = "Planner";
                            IndexDDLName = "DDLPlanner";
                            IndexTXTName = "TXTPlanner";
                            IndexCHKName = "CHKPlanner";
                        }
                        if (i == 7)
                        {
                            external.CIBType = "MCL";
                            IndexDDLName = "DDLMCL";
                            IndexTXTName = "TXTMCL";
                            IndexCHKName = "CHKMCL";
                        }
                        if (i == 8)
                        {
                            external.CIBType = "DocControl";
                            IndexDDLName = "DDLDocControl";
                            IndexTXTName = "TXTDocControl";
                            IndexCHKName = "CHKDocControl";
                        }
                        if (i == 9)
                        {
                            external.CIBType = "Program";
                            IndexDDLName = "DDLProgramLeader";
                            IndexTXTName = "TXTProgramLeader";
                            IndexCHKName = "CHKProgramLeader";
                        }
                        if (i == 10)
                        {
                            external.CIBType = "QAM";
                            IndexDDLName = "DDLQAM";
                            IndexTXTName = "TXTQAM";
                            IndexCHKName = "CHKQAM";
                        }
                        dr["CIBType"] = external.CIBType.ToString();
                        ContentPlaceHolder MainContent = Page.Master.FindControl("MainContent") as ContentPlaceHolder;

                        for (int l = 1; l <= 6; l++)
                        {

                            DropDownList myControl1 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name" + l);
                            // myControl1.Enabled = false;
                            if (myControl1 != null)
                            {
                                //  external.Name1 = myControl1.SelectedValue.ToString();
                                string Name = "Name" + l;
                                dr[Name] = myControl1.SelectedValue.ToString();
                                if (myControl1.SelectedValue.ToString() != "")
                                {
                                    if (i == 1)
                                    {
                                        if (ENGCurrentApprover == "")
                                        {
                                            ENGCurrentApprover = "Name" + l;
                                            //ENGCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 2)
                                    {
                                        if (QACurrentApprover == "")
                                        {
                                            QACurrentApprover = "Name" + l;
                                            //QACurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 3)
                                    {
                                        if (NDTCurrentApprover == "")
                                        {
                                            NDTCurrentApprover = "Name" + l;
                                            //NDTCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 4)
                                    {
                                        if (SPCPROCurrentApprover == "")
                                        {
                                            SPCPROCurrentApprover = "Name" + l;
                                            //SPCPROCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 5)
                                    {
                                        if (PURCurrentApprover == "")
                                        {
                                            PURCurrentApprover = "Name" + l;
                                            //PURCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 6)
                                    {
                                        if (PLANNERCurrentApprover == "")
                                        {
                                            PLANNERCurrentApprover = "Name" + l;
                                            //PLANNERCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 7)
                                    {
                                        if (MCLCurrentApprover == "")
                                        {
                                            MCLCurrentApprover = "Name" + l;
                                            //MCLCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 8)
                                    {
                                        if (DOCCONTROLCurrentApprover == "")
                                        {
                                            DOCCONTROLCurrentApprover = "Name" + l;
                                            //DOCCONTROLCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 9)
                                    {
                                        if (PROGRAMCONTROLCurrentApprover == "")
                                        {
                                            PROGRAMCONTROLCurrentApprover = "Name" + l;
                                            //PROGRAMCONTROLCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                    if (i == 10)
                                    {
                                        if (QAMCurrentApprover == "")
                                        {
                                            QAMCurrentApprover = "Name" + l;
                                            //QAMCurrentApprover = myControl1.SelectedValue.ToString();
                                            Depth = i.ToString();

                                        }
                                    }
                                }

                            }
                        }
                        for (int l = 1; l <= 6; l++)
                        {

                            DropDownList myControlAction1 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired" + l);
                            if (myControlAction1 != null)
                            {
                                string ActionRequired = "ActionRequired" + l;
                                dr[ActionRequired] = myControlAction1.SelectedValue.ToString();
                            }
                        }

                        for (int l = 1; l <= 11; l++)
                        {
                            CheckBox myControlchkreview = (CheckBox)MainContent.FindControl(IndexCHKName + +l);
                            string Comments = "chkReview" + l;
                            if (myControlchkreview != null)
                            {
                                if (myControlchkreview.Checked == true)
                                {

                                    dr[Comments] = "1";
                                }
                                else
                                {
                                    dr[Comments] = "0";
                                }
                            }
                        }
                        for (int l = 1; l <= 11; l++)
                        {
                            TextBox myControlComments1 = (TextBox)MainContent.FindControl(IndexTXTName + "Review" + l);
                            if (myControlComments1 != null)
                            {
                                if (!string.IsNullOrEmpty(myControlComments1.Text.ToString()))
                                //if (myControlComments1 != null || myControlComments1.Text!="")
                                {
                                    string Comments = "ReviewData" + l;
                                    dr[Comments] = myControlComments1.Text.ToString();
                                }
                            }
                        }
                        for (int l = 1; l <= 6; l++)
                        {


                            TextBox myControlDueDate1 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate" + l);

                            if (myControlDueDate1 != null)
                            {
                                if (!string.IsNullOrEmpty(myControlDueDate1.Text.ToString()))
                                {
                                    string DueDate = "Date" + l;
                                    //dr[DueDate] = myControlDueDate1.Text.ToString();
                                    dr[DueDate] = ToDbDate(myControlDueDate1.Text);

                                }

                            }
                        }
                        for (int l = 1; l <= 6; l++)
                        {
                            TextBox myControlComments1 = (TextBox)MainContent.FindControl(IndexTXTName + "Comment" + l);
                            if (myControlComments1 != null)
                            {
                                if (!string.IsNullOrEmpty(myControlComments1.Text.ToString()))
                                //if (myControlComments1 != null || myControlComments1.Text!="")
                                {
                                    string Comments = "Comment" + l;
                                    dr[Comments] = myControlComments1.Text.ToString();
                                }
                            }
                        }


                        dtExternalType.Rows.Add(dr);
                        //externalList.Add(external);



                    }
                    string Temp_num = User.Identity.Name.ToString() + DateTime.Now.ToString("dd/MM/yyyy HH:mm:ss", CultureInfo.InvariantCulture);
                    //for (int i=0;i<=externalList.Count;i++)
                    //{


                    //}
                    string msg = "";
                    try
                    {

                        using (SqlConnection con = new SqlConnection(constr))
                        {
                            using (SqlCommand cmd = new SqlCommand("SAM_DMW_External_Document_SP", con))
                            {
                                cmd.CommandType = CommandType.StoredProcedure;
                                con.Open();



                                cmd.Parameters.AddWithValue("@value0", DDLDoctype.SelectedValue.ToString());
                                cmd.Parameters.AddWithValue("@value1", Revision.Text.ToString());
                                cmd.Parameters.AddWithValue("@value2", TxtEffectiveDate.Text.ToString());
                                // cmd.Parameters.AddWithValue("@value3", "");
                                cmd.Parameters.AddWithValue("@value3", DDLRequester.SelectedValue.ToString());
                                cmd.Parameters.AddWithValue("@value4", ENGCurrentApprover.ToString()); //ENGcurrentApprover
                                cmd.Parameters.AddWithValue("@value5", txtCIBNumber.Text.ToString());
                                cmd.Parameters.AddWithValue("@value6", txtDocumentDesc.Text.ToString());
                                cmd.Parameters.AddWithValue("@value7", lblDRONo.Text.ToString());
                                cmd.Parameters.AddWithValue("@value8", TxtComment.Text.ToString());
                                cmd.Parameters.AddWithValue("@value9", TxtRevision.Text.ToString());
                                cmd.Parameters.AddWithValue("@value10", txtRevisionDesc.Text.ToString());
                                cmd.Parameters.AddWithValue("@value11", User.Identity.Name.ToString());
                                cmd.Parameters.AddWithValue("@value12", "Submit");
                                cmd.Parameters.AddWithValue("@value13", DDLCustomer.SelectedValue.ToString());
                                cmd.Parameters.AddWithValue("@value14", "Open");
                                cmd.Parameters.AddWithValue("@value15", 1); //depth
                                cmd.Parameters.AddWithValue("@value16", User.Identity.Name.ToString() + TempDate.ToString());
                                cmd.Parameters.AddWithValue("@value17", QACurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value18", NDTCurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value19", SPCPROCurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value20", PURCurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value21", PLANNERCurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value22", MCLCurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value23", DOCCONTROLCurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value24", PROGRAMCONTROLCurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value25", QAMCurrentApprover.ToString());
                                cmd.Parameters.AddWithValue("@value26", DDLUploadUser.SelectedValue.ToString());
                                cmd.Parameters.AddWithValue("@value27", Trans_num.ToString());


                                //cmd.Parameters.AddWithValue("@tblSAMDMWTempExternalType", dtExternalType);
                                var tvp = new SqlParameter("@tblSAMDMWTempExternalType", SqlDbType.Structured);
                                tvp.TypeName = "dbo.SAM_DMW_ExternalType"; // <- ต้องตรงกับชื่อ Table Type จริงใน DB
                                tvp.Value = dtExternalType;
                                cmd.Parameters.Add(tvp);




                                cmd.Parameters.Add("@Infobar", SqlDbType.VarChar, 1000);

                                cmd.Parameters["@Infobar"].Direction = ParameterDirection.Output;
                                try
                                {


                                    cmd.ExecuteNonQuery();
                                    //BindOtherActivity();

                                    if (cmd.Parameters["@Infobar"].Value != null)
                                    {

                                        msg = cmd.Parameters["@Infobar"].Value.ToString();


                                        if (msg != "Cannot Save Data." || msg != null)
                                        {
                                            Disable();
                                            messageVal = "Successfully Submitted!";
                                            try
                                            {

                                                string root = Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/");
                                                if (Directory.Exists(root))
                                                {
                                                    string[] files = Directory.GetFiles(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));


                                                    //if (FileUpload1.HasFiles)
                                                    if (files.Length > 0)
                                                    {

                                                        //string queryTrans_Num = "SELECT TOP 1 * FROM SAM_DMW_ExternalForm ORDER BY Trans_ID DESC";
                                                        //string Trans_Num = "";
                                                        //SqlConnection conn1 = new SqlConnection(constr);
                                                        //SqlCommand cmd1 = new SqlCommand(queryTrans_Num, conn1);
                                                        //conn1.Open();
                                                        //SqlDataReader dr1 = cmd1.ExecuteReader();
                                                        //while (dr1.Read())
                                                        //{
                                                        //    Trans_Num = dr1["Trans_Num"].ToString();
                                                        //}
                                                        //dr1.Close();
                                                        //conn1.Close();

                                                        if (!Directory.Exists(folderPath + Trans_num))
                                                        {
                                                            try
                                                            {
                                                                string userName = Environment.UserName;
                                                                //  CommonClass.writeLog(DateTime.Now.ToString() + "- " + userName + " - [beforecreate-FileUpload1.HasFiles] Error: " + folderPath + Trans_Num);
                                                                RClass.debug("Directory not exist: create path '" + folderPath + Trans_num + "'");
                                                                Directory.CreateDirectory(folderPath + Trans_num);
                                                                // CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [aftercretae-FileUpload1.HasFiles] Error: " + folderPath + Trans_Num);

                                                            }
                                                            catch (Exception ex)
                                                            {
                                                                //  CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [errorcretaepath-FileUpload1.HasFiles] Error: " + ex.Message);
                                                            }
                                                        }


                                                        // foreach (HttpPostedFile uploadedFile in FileUpload1.PostedFiles)
                                                        foreach (string file in files)
                                                        {
                                                            try
                                                            {
                                                                string destPath = System.IO.Path.Combine(folderPath + Trans_num, Path.GetFileName(file));
                                                                if (!System.IO.File.Exists(destPath))
                                                                {
                                                                    System.IO.File.Copy(file, destPath);
                                                                }
                                                                else
                                                                {
                                                                    // File already exists at destination -> skip copy to avoid unnecessary writes/duplicates
                                                                    RClass.debug("File already exists, skipping copy: " + destPath);
                                                                }
                                                            }
                                                            catch (Exception ex)
                                                            {
                                                                // CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [save fileupload-FileUpload1.HasFiles] Error: " + ex.Message);
                                                            }

                                                        }

                                                        var dir = new DirectoryInfo(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));
                                                        foreach (FileInfo file in dir.EnumerateFiles())
                                                        {
                                                            file.Delete();
                                                        }
                                                        dir.Delete();
                                                    }
                                                }
                                                BindGVFileUpload(folderPath + Trans_num);
                                                //if (FileUpload1.HasFiles)
                                                //{
                                                //    string Trans_Num = msg.ToString();
                                                //    //string queryTrans_Num = "SELECT TOP 1 * FROM SAM_DMW_ExternalForm ORDER BY Trans_ID DESC";

                                                //    //SqlConnection conn1 = new SqlConnection(constr);
                                                //    //SqlCommand cmd1 = new SqlCommand(queryTrans_Num, conn1);
                                                //    //conn1.Open();
                                                //    //SqlDataReader dr1 = cmd1.ExecuteReader();
                                                //    //while (dr1.Read())
                                                //    //{
                                                //    //    Trans_Num = dr1["Trans_Num"].ToString();
                                                //    //}
                                                //    //dr1.Close();
                                                //    //conn1.Close();
                                                //    if (!Directory.Exists(folderPath + Trans_Num))
                                                //    {
                                                //        try
                                                //        {
                                                //            string userName = Environment.UserName;
                                                //            //  CommonClass.writeLog(DateTime.Now.ToString() + "- " + userName + " - [beforecreate-FileUpload1.HasFiles] Error: " + folderPath + Trans_Num);
                                                //            RClass.debug("Directory not exist: create path '" + folderPath + Trans_Num + "'");
                                                //            Directory.CreateDirectory(folderPath + Trans_Num);
                                                //            // CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [aftercretae-FileUpload1.HasFiles] Error: " + folderPath + Trans_Num);

                                                //        }
                                                //        catch (Exception ex)
                                                //        {
                                                //            //  CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [errorcretaepath-FileUpload1.HasFiles] Error: " + ex.Message);
                                                //        }
                                                //    }

                                                //    //for mulitple file uploads
                                                //    foreach (HttpPostedFile uploadedFile in FileUpload1.PostedFiles)
                                                //    {
                                                //        try
                                                //        {
                                                //            if ((uploadedFile.FileName.Contains("xlsx")) || (uploadedFile.FileName.Contains("pdf")) || (uploadedFile.FileName.Contains("docx")))
                                                //            {
                                                //                RClass.debug("contains pdf");
                                                //                uploadedFile.SaveAs(System.IO.Path.Combine(folderPath + Trans_Num, uploadedFile.FileName));
                                                //                listofuploadedfiles.Text += String.Format("{0}<br />", Path.GetFileName(uploadedFile.FileName));
                                                //            }
                                                //        }
                                                //        catch (Exception ex)
                                                //        {
                                                //            // CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [save fileupload-FileUpload1.HasFiles] Error: " + ex.Message);
                                                //        }
                                                //        //if (uploadedFile.FileName.Contains("pdf"))
                                                //        //{
                                                //        //    RClass.debug("contains pdf");
                                                //        //    uploadedFile.SaveAs(System.IO.Path.Combine(folderPath + Trans_Num, uploadedFile.FileName));
                                                //        //    listofuploadedfiles.Text += String.Format("{0}<br />", Path.GetFileName(uploadedFile.FileName));
                                                //        //}
                                                //    }
                                                //    /*String filePath = folderPath + "/" + FileUpload1.FileName;
                                                //    FileUpload1.SaveAs(filePath);*/
                                                //}
                                                //  ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Successfully submitted.')", true);

                                            }
                                            catch (Exception ex)
                                            {
                                                // CommonClass.writeLog(DateTime.Now.ToString() + "- " + HttpContext.Current.User.Identity.Name + " - [failed  catch fileupload-FileUpload1.HasFiles] Error: " + ex.Message);
                                                RClass.insertAppExceptionLog(ex.Message.ToString(), User.Identity.Name);
                                                ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Data inserted successffuly in the database, but the file was not saved. Please contact the Administrator!.')", true);
                                                BtnUser1Submit.Enabled = false;
                                            }
                                        }

                                    }
                                    else
                                    {
                                        ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Cannot Create Trans_num Plaese contact administrator.')", true);
                                        //ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Data Cannot be insert')", true);
                                    }
                                }
                                catch (Exception ex)
                                { ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('" + ex.Message + "')", true); }
                                con.Close();
                            }
                        }
                    }
                    catch (Exception ex)
                    {


                    }


                }
                catch (Exception ex)
                {
                    LblMessage.Text = "Error while saving data." + ex.ToString();
                    RClass.insertAppExceptionLog(ex.ToString(), User.Identity.Name.ToString());
                }
            }
            else
            {
                if (string.IsNullOrWhiteSpace(LblMessage.Text))
                {
                    messageVal = "There is an Un-Closed transaction for this Request!";
                }
                LblMessage.Text = messageVal;
            }

            ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('" + messageVal + "')", true);

        }

        //DropDownList myControl1 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name1");
        //if (myControl1 != null)
        //{
        //    external.Name1 = myControl1.SelectedValue.ToString();
        //    dr["Name1"] = myControl1.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name1;
        //        Depth = i.ToString();

        //    }
        //}

        ////ContentPlaceHolder MainContent2 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl2 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name2");
        //if (myControl2 != null)
        //{
        //    external.Name2 = myControl2.SelectedValue.ToString();
        //    dr["Name2"] = myControl2.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name2;
        //        Depth = i.ToString();
        //    }
        //}

        ////ContentPlaceHolder MainContent3 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl3 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name3");
        //if (myControl3 != null)
        //{
        //    external.Name3 = myControl3.SelectedValue.ToString();
        //    dr["Name3"] = myControl3.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name3;
        //        Depth = i.ToString();
        //    }
        //}

        ////ContentPlaceHolder MainContent4 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl4 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name4");
        //if (myControl4 != null)
        //{
        //    external.Name4 = myControl4.SelectedValue.ToString();
        //    dr["Name4"] = myControl4.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name4;
        //        Depth = i.ToString();
        //    }
        //}

        //// ContentPlaceHolder MainContent5 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl5 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name5");
        //if (myControl5 != null)
        //{
        //    external.Name5 = myControl5.SelectedValue.ToString();
        //    dr["Name5"] = myControl5.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name5;
        //        Depth = i.ToString();
        //    }
        //}

        ////ContentPlaceHolder MainContent6 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl6 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name6");
        //if (myControl6 != null)
        //{
        //    external.Name6 = myControl6.SelectedValue.ToString();
        //    dr["Name6"] = myControl6.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name6;
        //        Depth = i.ToString();
        //    }
        //}

        ////ContentPlaceHolder MainContent7 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl7 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name7");
        //if (myControl7 != null)
        //{
        //    external.Name7 = myControl7.SelectedValue.ToString();
        //    dr["Name7"] = myControl7.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name7;
        //        Depth = i.ToString();
        //    }
        //}

        ////ContentPlaceHolder MainContent8 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl8 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name8");
        //if (myControl8 != null)
        //{
        //    external.Name8 = myControl8.SelectedValue.ToString();
        //    dr["Name8"] = myControl8.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name8;
        //        Depth = i.ToString();
        //    }
        //}

        ////ContentPlaceHolder MainContent9 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl9 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name9");
        //if (myControl9 != null)
        //{
        //    external.Name9 = myControl9.SelectedValue.ToString();
        //    dr["Name9"] = myControl9.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name9;
        //        Depth = i.ToString();
        //    }
        //}

        ////ContentPlaceHolder MainContent10 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControl10 = (DropDownList)MainContent.FindControl(IndexDDLName + "Name10");
        //if (myControl10 != null)
        //{
        //    external.Name10 = myControl10.SelectedValue.ToString();
        //    dr["Name10"] = myControl10.SelectedValue.ToString();
        //    if (CurrentApprover == "")
        //    {
        //        CurrentApprover = external.Name10;
        //        Depth = i.ToString();
        //    }
        //}


        //   ContentPlaceHolder MainContentAction1 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction1 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired1");
        //if (myControlAction1 != null)
        //{
        //    external.ActionRequired1 = myControlAction1.SelectedValue.ToString();
        //    dr["ActionRequired1"] = myControlAction1.SelectedValue.ToString();
        //}

        ////   ContentPlaceHolder MainContentAction2 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction2 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired2");
        //if (myControlAction2 != null)
        //{
        //    external.ActionRequired2 = myControlAction2.SelectedValue.ToString();
        //    dr["ActionRequired2"] = myControlAction2.SelectedValue.ToString();
        //}

        ////  ContentPlaceHolder MainContentAction3 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction3 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired3");
        //if (myControlAction3 != null)
        //{
        //    external.ActionRequired3 = myControlAction3.SelectedValue.ToString();
        //    dr["ActionRequired3"] = myControlAction3.SelectedValue.ToString();
        //}

        ////  ContentPlaceHolder MainContentAction4 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction4 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired4");
        //if (myControlAction4 != null)
        //{
        //    external.ActionRequired4 = myControlAction4.SelectedValue.ToString();
        //    dr["ActionRequired4"] = myControlAction4.SelectedValue.ToString();
        //}

        //// ContentPlaceHolder MainContentAction5 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction5 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired5");
        //if (myControlAction5 != null)
        //{
        //    external.ActionRequired5 = myControlAction5.SelectedValue.ToString();
        //    dr["ActionRequired5"] = myControlAction5.SelectedValue.ToString();
        //}

        //// ContentPlaceHolder MainContentAction6 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction6 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired6");
        //if (myControlAction6 != null)
        //{
        //    external.ActionRequired6 = myControlAction6.SelectedValue.ToString();
        //    dr["ActionRequired6"] = myControlAction6.SelectedValue.ToString();
        //}

        //// ContentPlaceHolder MainContentAction7 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction7 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired7");
        //if (myControlAction7 != null)
        //{
        //    external.ActionRequired7 = myControlAction7.SelectedValue.ToString();
        //    dr["ActionRequired7"] = myControlAction7.SelectedValue.ToString();
        //}

        //// ContentPlaceHolder MainContentAction8 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction8 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired8");
        //if (myControlAction8 != null)
        //{
        //    external.ActionRequired8 = myControlAction8.SelectedValue.ToString();
        //    dr["ActionRequired8"] = myControlAction8.SelectedValue.ToString();
        //}

        //// ContentPlaceHolder MainContentAction9 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction9 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired9");
        //if (myControlAction9 != null)
        //{
        //    external.ActionRequired9 = myControlAction9.SelectedValue.ToString();
        //    dr["ActionRequired9"] = myControlAction9.SelectedValue.ToString();
        //}

        //// ContentPlaceHolder MainContentAction10 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //DropDownList myControlAction10 = (DropDownList)MainContent.FindControl(IndexDDLName + "ActionRequired10");
        //if (myControlAction10 != null)
        //{
        //    external.ActionRequired10 = myControlAction10.SelectedValue.ToString();
        //    dr["ActionRequired10"] = myControlAction10.SelectedValue.ToString();
        //}


        //  ContentPlaceHolder MainContentDueDate1 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate1 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate1");

        //if (myControlDueDate1 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate1.Text.ToString()))
        //    {
        //        external.DueDate1 = myControlDueDate1.Text.ToString();
        //        dr["DueDate1"] = myControlDueDate1.Text.ToString();
        //    }

        //}

        //// ContentPlaceHolder MainContentDueDate2 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate2 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate2");
        //if (myControlDueDate2 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate2.Text.ToString()))
        //    {
        //        external.DueDate2 = myControlDueDate2.Text.ToString();
        //        dr["DueDate2"] = myControlDueDate2.Text.ToString();
        //    }
        //}

        ////   ContentPlaceHolder MainContentDueDate3 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate3 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate3");
        //if (myControlDueDate3 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate3.Text.ToString()))
        //    {
        //        external.DueDate3 = myControlDueDate3.Text.ToString();
        //        dr["DueDate3"] = myControlDueDate3.Text.ToString();
        //    }
        //}

        //// ContentPlaceHolder MainContentDueDate4 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate4 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate4");
        //if (myControlDueDate4 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate4.Text.ToString()))
        //    {
        //        dr["DueDate4"] = myControlDueDate4.Text.ToString();
        //        external.DueDate4 = myControlDueDate4.Text.ToString();
        //    }
        //}

        //// ContentPlaceHolder MainContentDueDate5 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate5 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate5");
        //if (myControlDueDate5 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate5.Text.ToString()))
        //    {
        //        dr["DueDate5"] = myControlDueDate5.Text.ToString();
        //        external.DueDate5 = myControlDueDate5.Text.ToString();
        //    }
        //}

        ////   ContentPlaceHolder MainContentDueDate6 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate6 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate6");
        //if (myControlDueDate6 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate6.Text.ToString()))
        //    {
        //        dr["DueDate6"] = myControlDueDate6.Text.ToString();
        //        external.DueDate6 = myControlDueDate6.Text.ToString();
        //    }
        //}

        ////   ContentPlaceHolder MainContentDueDate7 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate7 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate7");
        //if (myControlDueDate7 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate7.Text.ToString()))
        //    {
        //        dr["DueDate7"] = myControlDueDate7.Text.ToString();
        //        external.DueDate7 = myControlDueDate7.Text.ToString();
        //    }
        //}

        ////    ContentPlaceHolder MainContentDueDate8 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate8 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate8");
        //if (myControlDueDate8 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate8.Text.ToString()))
        //    {
        //        dr["DueDate8"] = myControlDueDate8.Text.ToString();
        //        external.DueDate8 = myControlDueDate8.Text.ToString();
        //    }
        //}

        ////  ContentPlaceHolder MainContentDueDate9 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate9 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate9");
        //if (myControlDueDate9 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate9.Text.ToString()))
        //    {
        //        dr["DueDate9"] = myControlDueDate9.Text.ToString();
        //        external.DueDate9 = myControlDueDate9.Text.ToString();
        //    }
        //}

        ////  ContentPlaceHolder MainContentDueDate10 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //TextBox myControlDueDate10 = (TextBox)MainContent.FindControl(IndexTXTName + "DueDate10");
        //if (myControlDueDate10 != null)
        //{
        //    if (!string.IsNullOrEmpty(myControlDueDate10.Text.ToString()))
        //    {
        //        dr["DueDate10"] = myControlDueDate10.Text.ToString();
        //        external.DueDate10 = myControlDueDate10.Text.ToString();
        //    }
        //}
        //    TextBox myControlComments1 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments1");
        //    if (myControlComments1!=null)
        //    {
        //    if (!string.IsNullOrEmpty(myControlComments1.Text.ToString()))
        //    //if (myControlComments1 != null || myControlComments1.Text!="")
        //    {
        //        external.Comments1 = myControlComments1.Text.ToString();
        //        dr["Comments1"] = myControlComments1.Text.ToString();
        //    }
        //}

        //    // ContentPlaceHolder MainContentDueDate2 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments2 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments2");
        //    if (myControlComments2 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments2.Text.ToString()))
        //        {
        //            external.Comments2 = myControlComments2.Text.ToString();
        //            dr["Comments2"] = myControlComments2.Text.ToString();
        //        }
        //    }
        //    //   ContentPlaceHolder MainContentDueDate3 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments3 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments3");
        //    if (myControlComments3 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments3.Text.ToString()))
        //        {
        //            external.Comments3 = myControlComments3.Text.ToString();
        //            dr["Comments3"] = myControlComments3.Text.ToString();
        //        }
        //    }

        //    // ContentPlaceHolder MainContentDueDate4 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments4 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments4");
        //    if (myControlComments4 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments4.Text.ToString()))
        //        {
        //            dr["Comments4"] = myControlComments4.Text.ToString();
        //            external.Comments4 = myControlComments4.Text.ToString();
        //        }
        //    }

        //    // ContentPlaceHolder MainContentDueDate5 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments5 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments5");
        //    if (myControlComments5 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments5.Text.ToString()))
        //        {
        //            dr["Comments5"] = myControlComments5.Text.ToString();
        //            external.Comments5 = myControlComments5.Text.ToString();
        //        }
        //    }

        //    //   ContentPlaceHolder MainContentDueDate6 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments6 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments6");
        //    if (myControlComments6 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments6.Text.ToString()))
        //        {
        //            dr["Comments6"] = myControlComments6.Text.ToString();
        //            external.Comments6 = myControlComments6.Text.ToString();
        //        }
        //    }

        //    //   ContentPlaceHolder MainContentDueDate7 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments7 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments7");
        //    if (myControlComments7 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments7.Text.ToString()))
        //        {
        //            dr["Comments7"] = myControlComments7.Text.ToString();
        //            external.Comments7 = myControlComments7.Text.ToString();
        //        }
        //    }

        //    //    ContentPlaceHolder MainContentDueDate8 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments8 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments8");
        //    if (myControlComments8 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments8.Text.ToString()))
        //        {
        //            dr["Comments8"] = myControlComments8.Text.ToString();
        //            external.Comments8 = myControlComments8.Text.ToString();
        //        }
        //    }

        //    //  ContentPlaceHolder MainContentDueDate9 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments9 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments9");
        //    if (myControlComments9 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments9.Text.ToString()))
        //        {
        //            dr["Comments9"] = myControlComments9.Text.ToString();
        //            external.Comments9 = myControlComments9.Text.ToString();
        //        }
        //    }

        //    //  ContentPlaceHolder MainContentDueDate10 = Page.Master.FindControl("MainContent") as ContentPlaceHolder;
        //    TextBox myControlComments10 = (TextBox)MainContent.FindControl(IndexTXTName + "Comments10");
        //    if (myControlComments10 != null)
        //    {
        //        if (!string.IsNullOrEmpty(myControlComments10.Text.ToString()))
        //        {
        //            dr["Comments10"] = myControlComments10.Text.ToString();
        //            external.Comments10 = myControlComments10.Text.ToString();
        //        }
        //    }


        //dtExternalType.Rows.Add(dr);
        //externalList.Add(external);
        protected void DownloadFile(object sender, EventArgs e)
        {
            //string filePath = (sender as ImageButton).CommandArgument;
            //Response.ContentType = ContentType;
            //Response.AppendHeader("Content-Disposition", "attachment; filename=" + Path.GetFileName(filePath));
            //Response.WriteFile(filePath);
            //Response.End();

            try
            {
                string filePath = (sender as ImageButton).CommandArgument;
                Response.ContentType = ContentType;
                Response.AppendHeader("Content-Disposition", "attachment; filename=" + Path.GetFileName(filePath));
                Response.WriteFile(filePath);
                Response.End();
                //filePath = @"\\sam32\Intranet\Public\ESA Awareness Training Webcast 2024-01-04.pdf";
                //HttpCookie cookie = new HttpCookie("tempFilePath");
                //cookie.Value = filePath;
                //cookie.Expires = DateTime.Now.AddMinutes(15);
                //Response.Cookies.Add(cookie);
                //Admin cs = new Admin();
                //cs.ProcessRequest(this.Context);
                //  ScriptManager.RegisterStartupScript(this, this.GetType(), "alert", "window.location ='./Admin.cs';", true);
            }
            catch (Exception ex)
            {
                //Debug.WriteLine(ex.ToString());
            }
        }
        protected void BindGVFileUpload(string tmpPath)
        {
            GVAttachment.DataSource = RClass.LoadFile(tmpPath);
            GVAttachment.DataBind();
        }
        protected void DeleteFile(object sender, EventArgs e)
        {
            string filePath = (sender as ImageButton).CommandArgument;
            RClass.DeleteFile(filePath);
            BindGVFileUpload(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));
            //GVAttachment.DataSource = RClass.LoadFile(Server.MapPath("~/Uploads1/" + LblGuid.Text.ToString() + "/"));
            //GVAttachment.DataBind();
        }
        protected void BtnUpdate_Click(object sender, EventArgs e)
        {
            string constr = ConfigurationManager.ConnectionStrings["ConnStringDbLive"].ConnectionString;
            LblMessage.Text = "";
            query = "SELECT COUNT(1) FROM SAM_DMW_QAForm WHERE Trans_Num = @value0";
            string Trans_Num = Request.QueryString["ID"].ToString();
            values = Trans_Num + "|";
            if (dbClass.CheckExists(query, values))
            {
                try
                {
                    query = "SAM_DMW_Document_SP @value0, @value1, @value2, @value3, @value4, @value5, @value6, @value7, @value8, @value9, @value10, @value11";
                    values = DDLDoctype.SelectedValue + "|" + DDLDoctype.SelectedValue.Replace(" ", "") + "||||" + Revision.Text + "|" + TxtEffectiveDate.Text + "|"
                + CheckBox2.Checked + "|||" + DDLRequester.SelectedValue + "|" + TxtComment.Text + "|" + "Update" + "|" + Trans_Num + "|";
                    dbClass.InsertUpdateDelete(query, values);
                    Disable();

                    ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", "alert('Successfully submitted.')", true);
                    if (FileUpload1.HasFiles)
                    {
                        //var folderPath = Server.MapPath("~/SharedDrive/" + Trans_Num);
                        if (!Directory.Exists(folderPath + Trans_Num))
                        {
                            Directory.CreateDirectory(folderPath + Trans_Num);
                        }

                        //for mulitple file uploads
                        foreach (HttpPostedFile uploadedFile in FileUpload1.PostedFiles)
                        {
                            if (uploadedFile.FileName.Contains("pdf"))
                            {
                                uploadedFile.SaveAs(System.IO.Path.Combine(folderPath + Trans_Num, uploadedFile.FileName));
                                //listofuploadedfiles.Text += String.Format("{0}<br />", uploadedFile.FileName);
                            }
                        }
                        BindGVFileUpload(folderPath + Trans_Num);
                    }
                }
                catch (Exception ex)
                {
                    LblMessage.Text = "Error while saving data." + ex.ToString();
                }
            }
            else
                LblMessage.Text = "There is no such request in the database!";

        }


        protected void BtnClear_Click(object sender, EventArgs e)
        {
            GVAttachment.DataSource = null;
            GVAttachment.DataBind();
            LblMessage.Text = "";
            DDLDoctype.ClearSelection();
            // DDLProgram.ClearSelection();
            Revision.Text = "";
            // ProcRevision.Text = "";
            //PartNo.Text = "";
            //DDLPartNo.ClearSelection();
            //DDLOperNo.ClearSelection();
            TxtEffectiveDate.Text = string.Empty;
            CheckBox2.Checked = false;
            //DDLInitiator.ClearSelection();
            DDLRequester.ClearSelection();
            TxtComment.Text = "";
        }

        protected void Disable()
        {
            //  Status.Text = "Pending Approval";
            DDLDoctype.Enabled = false;
            //   DDLProgram.Enabled = false;
            //PartNo.Enabled = false;
            // DDLPartNo.Enabled = false;
            // DDLOperNo.Enabled = false;
            FileUpload1.Enabled = false;
            Revision.Enabled = false;
            // ProcRevision.Enabled = false;
            // DDLInitiator.Enabled = false;
            DDLRequester.Enabled = false;
            TxtEffectiveDate.Enabled = false;
           
            CheckBox2.Enabled = false;
            //  Status.Enabled = false;
            TxtComment.Enabled = false;
            BtnClear.Enabled = false;
            BtnSubmit.Enabled = false;
            BtnUpdate.Enabled = false;
            BtnUser1Submit.Enabled = false; // also disable the user-level submit button for requester
        }

        protected void PartNo_TextChanged(object sender, EventArgs e)
        {
            //RClass.BindDDL(DDLOperNo, SPName, "OperNo|" + PartNo.Text);
        }

        protected void DisableForUpdate()
        {
            // Status.Text = "Pending Approval";
            DDLDoctype.Enabled = false;

            DDLRequester.Enabled = false;
            TxtEffectiveDate.Enabled = false;
            TxtEffectiveDate.Enabled = false;
            CheckBox2.Enabled = false;
            //Status.Enabled = false;
            // BtnUpdate.Visible = true;
            //BtnSubmit.Visible = false;
        }

        protected void DDLDocTypeOnSelectedIndexChanged(object sender, EventArgs e)
        {
            GetPrevRevision();

        }

        protected void DDLCustomer_SelectedIndexChanged(object sender, EventArgs e)
        {
            GetPrevRevision();
            // DisableCategory();
        }
        protected void TxtCIBNUmberOnTextChanged(object sender, EventArgs e)
        {
            GetPrevRevision();
        }
        //        protected void GetPrevRevision()
        //        {
        //            string PrevRevision_query = "select Revision from SAM_DMW_ExternalForm where Delete_Record is null and customer='" + DDLCustomer.SelectedValue.ToString()+"' and Document_Type='" + DDLDoctype.SelectedValue.ToString() + "'  and DocumentNo='" + txtDocumentNumber.Text.ToString() + "' order by Revision desc";
        //           // string PrevRevision_query = "select Revision from SAM_DMW_QAForm where Delete_Record is null and Document_Type='" + DDLDoctype.SelectedValue.ToString() + "' and Program='" + DDLProgram.SelectedValue.ToString() + "'  order by Revision desc";
        //            DataTable Requester_dt = dbClass.LoadData(PrevRevision_query, "");
        //            if (Requester_dt.Rows.Count > 0)
        //            {
        //                //  txtPrevRevision.Text = Requester_dt.Rows[0]["Revision"].ToString();
        //                // string Indexletter = Requester_dt.Rows[0]["Revision"].ToString().Substring(0, 1);
        //                 int getNextRevisonNum =Convert.ToInt32 (Requester_dt.Rows[0]["Revision"].ToString())+1;
        //               // int getNextRevisonNum = Convert.ToInt32(Requester_dt.Rows[0]["Revision"].ToString().Remove(0, 1));
        //                Revision.Text =  getNextRevisonNum.ToString().PadLeft(2,'0');
        //                //Revision.Text = RevNum.ToString();
        //}
        //            else
        //            {
        //                Revision.Text = "01";

        //            }

        //        }


        protected void DDLOperNum_SelectedIndexChanged(object sender, EventArgs e)
        {
            // GetPrevRevision();
        }

        protected void ddlActivityOnSelectedIndexChanged(object sender, EventArgs e)
        {
            ChangeActivity();
        }


        protected void DDLPartNo_SelectedIndexChanged(object sender, EventArgs e)
        {
            RClass.debug("Populate OperNo");
            //RClass.BindDDL(DDLOperNo, SPName, "OperNo|" + DDLPartNo.SelectedValue);
            // GetPrevRevision();
        }

        ///20260121///User infromed user ever reject and button showing but my version don't
        ///I cannot file the root of case I adding as below about it. 
        ///

        protected void BtnResubmit_Click(object sender, EventArgs e)
        {
            string transNum = (Request.QueryString["ID"] ?? "").Trim();
            if (string.IsNullOrEmpty(transNum))
            {
                ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert",
                    "alert('Resubmit ต้องเข้ามาจากงานเดิม (มี ID) เท่านั้น')", true);
                return;
            }

            // 1) โหลดสถานะล่าสุดจาก DB กัน user เปิดค้างไว้แล้ว status เปลี่ยน
            var dtCheck = dbClass.LoadData(
                "SELECT Status FROM dbo.SAM_DMW_ExternalForm WHERE Trans_Num=@value0", transNum);

            string status = (dtCheck.Rows.Count > 0 ? (dtCheck.Rows[0]["Status"] ?? "").ToString().Trim() : "");

            bool isRejected = status.Equals("Rejected", StringComparison.OrdinalIgnoreCase)
                           || status.Equals("Reject", StringComparison.OrdinalIgnoreCase);

            if (!isRejected)
            {
                ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert",
                    "alert('Resubmit ได้เฉพาะงานที่เป็น Rejected เท่านั้น')", true);
                return;
            }

            // 2) สร้าง dtExternalType จากหน้าจอ (คุณมี logic นี้อยู่แล้วใน BtnSubmit_Click)
            string tempDate = DateTime.Now.ToString("ddMMyyyyHHmmssffffff");
            DataTable dtExternalType = new DataTable();
            dtExternalType = dbClass.Externaltable(dtExternalType);

            // *** ตรงนี้ให้ใช้โค้ด loop เดิมของคุณ เพื่อ fill dtExternalType + หา ENGCurrentApprover ฯลฯ ***
            // สำคัญ: ตอนเริ่ม flow ใหม่ ให้ตั้ง Depth = 1 และ CurrentApprover เริ่มที่ Dept1 (เช่น Engineering Name1)
            string ENGCurrentApprover = "";
            string QACurrentApprover = "";
            string NDTCurrentApprover = "";
            string SPCPROCurrentApprover = "";
            string PURCurrentApprover = "";
            string PLANNERCurrentApprover = "";
            string MCLCurrentApprover = "";
            string DOCCONTROLCurrentApprover = "";
            string PROGRAMCONTROLCurrentApprover = "";
            string QAMCurrentApprover = "";

            // TODO: วาง loop i=1..10 ของคุณตรงนี้ (เหมือน BtnSubmit_Click) เพื่อเติมค่าให้ครบ

            // 3) อัปเดต ExternalForm ให้กลับไป Open + Depth 1 + current approver เริ่มใหม่
            // แนะนำทำผ่าน SP จะปลอดภัยที่สุด แต่ถ้ายังไม่มี SP ก็ทำ UPDATE ได้
            string updateFormSql = @"
UPDATE dbo.SAM_DMW_ExternalForm
SET
    Status = 'Open',
    Depth = 1,
    ENGCurrent_Approver_ID = @eng,
    QACurrent_Approver_ID = @qa,
    NDTCurrent_Approver_ID = @ndt,
    SPCPROCurrent_Approver_ID = @sp,
    PURCurrent_Approver_ID = @pur,
    PLANNERCurrent_Approver_ID = @pln,
    MCLCurrent_Approver_ID = @mcl,
    DOCCONTROLCurrent_Approver_ID = @doc,
    PROGRAMCurrent_Approver_ID = @prog,
    QAMCurrent_Approver_ID = @qam,
    UpdatedBy = @u,
    UpdateDate = GETDATE()
WHERE Trans_Num = @t;";

            using (var con = new SqlConnection(ConfigurationManager.ConnectionStrings["ConnStringDbLive"].ConnectionString))
            using (var cmd = new SqlCommand(updateFormSql, con))
            {
                cmd.Parameters.AddWithValue("@t", transNum);
                cmd.Parameters.AddWithValue("@u", User.Identity.Name.ToString());

                cmd.Parameters.AddWithValue("@eng", (object)ENGCurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@qa", (object)QACurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@ndt", (object)NDTCurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@sp", (object)SPCPROCurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@pur", (object)PURCurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@pln", (object)PLANNERCurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@mcl", (object)MCLCurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@doc", (object)DOCCONTROLCurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@prog", (object)PROGRAMCONTROLCurrentApprover ?? DBNull.Value);
                cmd.Parameters.AddWithValue("@qam", (object)QAMCurrentApprover ?? DBNull.Value);

                con.Open();
                cmd.ExecuteNonQuery();
            }

            
            // On Resubmit: do NOT delete existing SAM_DMW_EXTERNALTYPE; load existing rows and reuse them so unchanged data/files are preserved.
            try
            {
                DataTable dtExistingExt = dbClass.LoadData("SELECT * FROM dbo.SAM_DMW_EXTERNALTYPE WHERE Trans_Num=@value0", transNum);
                if (dtExistingExt.Rows.Count > 0)
                {
                    dtExternalType.Clear();
                    foreach (DataRow r in dtExistingExt.Rows)
                    {
                        DataRow nr = dtExternalType.NewRow();
                        foreach (DataColumn c in dtExternalType.Columns)
                        {
                            if (dtExistingExt.Columns.Contains(c.ColumnName) && r[c.ColumnName] != DBNull.Value)
                                nr[c.ColumnName] = r[c.ColumnName];
                        }
                        dtExternalType.Rows.Add(nr);
                    }
                }

                // Reset approval-related columns so workflow truly restarts (clear Status, Date, Comment columns)
                foreach (DataRow rr in dtExternalType.Rows)
                {
                    for (int si = 1; si <= 10; si++)
                    {
                        string statusCol = "Status" + si;
                        if (dtExternalType.Columns.Contains(statusCol))
                            rr[statusCol] = "";
                        string dateCol = "Date" + si;
                        if (dtExternalType.Columns.Contains(dateCol))
                            rr[dateCol] = DBNull.Value;
                        string commentCol = "Comment" + si;
                        if (dtExternalType.Columns.Contains(commentCol))
                            rr[commentCol] = DBNull.Value;
                    }
                }

                // Determine current approver columns for each department based on the FIRST available Name# column
                Func<string, string> GetFirstNameColumn = (dept) =>
                {
                    foreach (DataRow r2 in dtExternalType.Rows)
                    {
                        if (!r2.Table.Columns.Contains("CIBType")) continue;
                        if ((r2["CIBType"] ?? "").ToString().Equals(dept, StringComparison.OrdinalIgnoreCase))
                        {
                            for (int n = 1; n <= 3; n++)
                            {
                                string nameCol = "Name" + n;
                                if (r2.Table.Columns.Contains(nameCol) && r2[nameCol] != DBNull.Value && !string.IsNullOrWhiteSpace(r2[nameCol].ToString()))
                                {
                                    return nameCol; // e.g., "Name1"
                                }
                            }
                        }
                    }
                    return "";
                };

                // Load stored current approver columns (fallback) but then override to first Name if present so the workflow restarts from the first approver
                DataTable dtForm = dbClass.LoadData("SELECT ENGCurrent_Approver_ID,QACurrent_Approver_ID,NDTCurrent_Approver_ID,SPCPROCurrent_Approver_ID,PURCurrent_Approver_ID,PLANNERCurrent_Approver_ID,MCLCurrent_Approver_ID,DOCCONTROLCurrent_Approver_ID,PROGRAMCurrent_Approver_ID,QAMCurrent_Approver_ID FROM dbo.SAM_DMW_ExternalForm WHERE Trans_Num=@value0", transNum);
                if (dtForm.Rows.Count > 0)
                {
                    ENGCurrentApprover = (dtForm.Rows[0]["ENGCurrent_Approver_ID"] ?? "").ToString();
                    QACurrentApprover = (dtForm.Rows[0]["QACurrent_Approver_ID"] ?? "").ToString();
                    NDTCurrentApprover = (dtForm.Rows[0]["NDTCurrent_Approver_ID"] ?? "").ToString();
                    SPCPROCurrentApprover = (dtForm.Rows[0]["SPCPROCurrent_Approver_ID"] ?? "").ToString();
                    PURCurrentApprover = (dtForm.Rows[0]["PURCurrent_Approver_ID"] ?? "").ToString();
                    PLANNERCurrentApprover = (dtForm.Rows[0]["PLANNERCurrent_Approver_ID"] ?? "").ToString();
                    MCLCurrentApprover = (dtForm.Rows[0]["MCLCurrent_Approver_ID"] ?? "").ToString();
                    DOCCONTROLCurrentApprover = (dtForm.Rows[0]["DOCCONTROLCurrent_Approver_ID"] ?? "").ToString();
                    PROGRAMCONTROLCurrentApprover = (dtForm.Rows[0]["PROGRAMCurrent_Approver_ID"] ?? "").ToString();
                    QAMCurrentApprover = (dtForm.Rows[0]["QAMCurrent_Approver_ID"] ?? "").ToString();
                }

                // Override to first Name column to restart the approval flow at the first approver (Name1 if available)
                try
                {
                    string engFirst = GetFirstNameColumn("Engineering"); if (!string.IsNullOrEmpty(engFirst)) ENGCurrentApprover = engFirst;
                    string qaFirst = GetFirstNameColumn("QA"); if (!string.IsNullOrEmpty(qaFirst)) QACurrentApprover = qaFirst;
                    string ndtFirst = GetFirstNameColumn("NDT"); if (!string.IsNullOrEmpty(ndtFirst)) NDTCurrentApprover = ndtFirst;
                    string spFirst = GetFirstNameColumn("SpecialProcess"); if (!string.IsNullOrEmpty(spFirst)) SPCPROCurrentApprover = spFirst;
                    string purFirst = GetFirstNameColumn("Purchasing"); if (!string.IsNullOrEmpty(purFirst)) PURCurrentApprover = purFirst;
                    string plannerFirst = GetFirstNameColumn("Planner"); if (!string.IsNullOrEmpty(plannerFirst)) PLANNERCurrentApprover = plannerFirst;
                    string mclFirst = GetFirstNameColumn("MCL"); if (!string.IsNullOrEmpty(mclFirst)) MCLCurrentApprover = mclFirst;
                    string docFirst = GetFirstNameColumn("DocControl"); if (!string.IsNullOrEmpty(docFirst)) DOCCONTROLCurrentApprover = docFirst;
                    string progFirst = GetFirstNameColumn("Program"); if (!string.IsNullOrEmpty(progFirst)) PROGRAMCONTROLCurrentApprover = progFirst;
                    string qamFirst = GetFirstNameColumn("QAM"); if (!string.IsNullOrEmpty(qamFirst)) QAMCurrentApprover = qamFirst;
                }
                catch (Exception ex)
                {
                    RClass.insertAppExceptionLog("Resubmit determine first approver error: " + ex.ToString(), User.Identity.Name);
                }
            }
            catch (Exception ex)
            {
                RClass.insertAppExceptionLog("Resubmit load existing ExternalType error: " + ex.ToString(), User.Identity.Name);
            }

            //  SP  insert ExternalType
            using (var con = new SqlConnection(ConfigurationManager.ConnectionStrings["ConnStringDbLive"].ConnectionString))
            using (var cmd = new SqlCommand("SAM_DMW_External_Document_SP", con))
            {
                cmd.CommandType = CommandType.StoredProcedure;
                con.Open();

                cmd.Parameters.AddWithValue("@value12", "Resubmit");  
                cmd.Parameters.AddWithValue("@value14", "Open");      
                cmd.Parameters.AddWithValue("@value15", 1);          

                cmd.Parameters.AddWithValue("@value27", transNum);
                //cmd.Parameters.AddWithValue("@tblSAMDMWTempExternalType", dtExternalType);

                var p = cmd.Parameters.Add("@tblSAMDMWTempExternalType", SqlDbType.Structured);
p.TypeName = "dbo.SAM_DMW_ExternalType";
p.Value = dtExternalType;



                cmd.Parameters.Add("@Infobar", SqlDbType.VarChar, 1000).Direction = ParameterDirection.Output;

                cmd.ExecuteNonQuery();

                string msg = (cmd.Parameters["@Infobar"].Value ?? "Resubmit done").ToString();
                ScriptManager.RegisterClientScriptBlock(this, this.GetType(), "alert", $"alert('{msg}')", true);
            }

            // 6) reload หน้าด้วยค่าใหม่
            Response.Redirect(Request.RawUrl, false);
        }

        private void ForceEnableSubmitOnlyForRejectedOwner()
        {
            if (dt == null || dt.Rows.Count == 0) return;

            string status = (dt.Rows[0]["Status"] ?? "").ToString().Trim();
            if (!status.Equals("Rejected", StringComparison.OrdinalIgnoreCase))
                return;

            // Only Requester (not uploader) can resubmit a rejected item
            string requester = (dt.Rows[0]["Requester"] ?? "").ToString().Trim();
            string loginUser = (User.Identity.Name ?? "").Trim();

            if (!requester.Equals(loginUser, StringComparison.OrdinalIgnoreCase))
                return; // not the Requester

            // enable resubmit for Requester
            BtnResubmit.Visible = true;
            BtnResubmit.Enabled = true;

            // ensure the button is enabled client-side too
            BtnResubmit.Attributes.Remove("disabled");
        }

        static object ToDbDate(string s)
        {
            s = (s ?? "").Trim();
            if (s == "") return DBNull.Value;

            // รองรับ input type="date" => yyyy-MM-dd
            if (DateTime.TryParseExact(s, "yyyy-MM-dd",
                CultureInfo.InvariantCulture, DateTimeStyles.None, out var d1))
                return d1;

            // เผื่อบางจอเป็น dd/MM/yyyy
            if (DateTime.TryParseExact(s, "dd/MM/yyyy",
                CultureInfo.InvariantCulture, DateTimeStyles.None, out var d2))
                return d2;

            return DBNull.Value; // กัน SQL พัง
        }


    }
}
