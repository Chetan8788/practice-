// chetan patil - [21/07/2023] - Rate revision page
import { TextField } from "../../common/TextField/TextField";
import { TextArea } from "../../common/TextArea/TextArea";
import "./RateRevision.css";
import Grid from "@mui/material/Unstable_Grid2";
import { yesNoList } from "../../constants/constants";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import { setInputBoxValueRateRevision } from "../../actions/raterevision";
import { Submit } from "../Submit/Submit";
import Select from "react-select";
import { useLocation } from "react-router";
import { useEffect } from "react";

export const RateRevision: React.FC = () => {
  const dispatch = useAppDispatch();
  const currentRateRevisionData = useAppSelector(
    (state: RootState) => state?.rateRevision?.rateRevisionData
  );
  const location = useLocation();

  const onValueChange = (key: any, value: any) => {
    dispatch(setInputBoxValueRateRevision(key, value));
  };

  // function onSubmitClick() {
  //   const candidateDataToSend: typeof EMPTY_CANDIDATE_DATA = {
  //     firstName: currentCandidateData.firstName,
  //     middleName: currentCandidateData.middleName,
  //     lastName: currentCandidateData.lastName,
  //     line1: currentCandidateData.line1,
  //     line2: currentCandidateData.line2,
  //     city: currentCandidateData.city,
  //     state: currentCandidateData.state.value,
  //     zipCode: currentCandidateData.zipCode,
  //     country: currentCandidateData.country,
  //     email: currentCandidateData.email,
  //     contactNumber: currentCandidateData.contactNumber,
  //     workAuthorization: currentCandidateData.workAuthorization.value,
  //     workAuthorizationExpiryDate: currentCandidateData.workAuthorizationExpiryDate,
  //   }
  //   dispatch(sendAllData(candidateDataToSend, currentClientData, currentVendorData, currentReferralData, currentJobData, currentBGCData, currentDocumentationData, currentStartEndOperationsData, currentRateRevisionData));
  // }

  return (
    <>
      {/* <Grid container spacing={4}>
        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={6} md={3}>
         
        </Grid>

        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={6} md={3}>
         
        </Grid>

        <Grid xs={6} md={3}>
         
        </Grid>

        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={6} md={3}>
          
        </Grid>

        <Grid xs={3} md={12}>
         
        </Grid>

        <Submit />
      </Grid> */}
      Rate revision details
      <div className="flex gap-5 " style={{ margin: "auto", width: "100%" }}>
        <div className="relative w-[100%] mt-10 border border-solid">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" className="px-6 py-3">
                  {/* <span> Rate revision</span> */}
                </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Gross BR</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.grossBr}
                    handleChange={(event) => {
                      onValueChange("grossBr", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>MSP fee in percentage</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.mspFeePercentage}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("mspFeePercentage", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>MSP fee</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.mspFee}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("mspFee", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Net bill rate</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.netBillRate}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("netBillRate", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Pay rate</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.payRate}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("payRate", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Referral fee</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.refFee}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("refFee", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Tax OH percentage</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.taxOHPercentage}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("taxOHPercentage", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div className="relative w-[100%] mt-10 border border-solid">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" className="px-6 py-3">
                  {/* <span> Rate revision</span> */}
                </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Opted for health benefits</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={yesNoList}
                    value={currentRateRevisionData?.optedForHB}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("optedForHB", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Tax OH</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.taxOH}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("taxOH", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Health benefits cost</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.healthB}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("healthB", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Net purchase</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.netPurchase}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("netPurchase", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Margin</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.margin}
                    // placeholder={""}
                    handleChange={(event) => {
                      onValueChange("margin", event?.target?.value);
                    }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Rate revision reason</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    // className="rate-revision-textarea"
                    value={currentRateRevisionData?.rateRevisionReason}
                    // placeholder={"Rate Revision Reason"}
                    handleChange={(event) => {
                      onValueChange("rateRevisionReason", event?.target?.value);
                    }}
                  />
                </td>
              </tr>
            </tbody>
          </table>
          {/* <Submit /> */}
        </div>
      </div>
      <Submit />
    </>
  );
};
