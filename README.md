import React from "react";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import { setVendorInputBoxValue } from "../../actions/vendor";
import {
  ContractType,
  LocationName,
  WorkAuthorization,
} from "../../constants/candidateclientconstants";
import Select from "react-select";
import { Typography } from "@mui/material";
import { EMPTY_ADDRESS_DATA } from "../../utils/addressutil";
import { setClientInputBoxValue } from "../../actions/client";
import { setJobInputBoxValue } from "../../actions/job";
import { setCandidateInputBoxValue } from "../../actions/candidate";
import ClientDetails from "../Client/ClientDetails";
import CandidateDetails from "./CandidateDetails";
import VendorDetails from "../Vendor/VendorDetails";
import JobDetails from "../Job/JobDetails";
import ReferralDetails from "../Referral/ReferralDetails";

// interface Props {
//     nextButtonClick: any;
//     setNextButtonClick: any;
//     setValid: any;
//     valid: any;
// }

const BasicDetails: React.FC = () => {
  // setNextButtonClick(false);
  // setValid(false);
  // const dispatch = useAppDispatch();
  // const currentCandidateData = useAppSelector((state: RootState) => state.candidate.candidateData);
  // const currentClientData = useAppSelector((state: RootState) => state.client.clientData);
  // const allClientData = useAppSelector((state: RootState) => state.client.allClientData);
  // let allClientName: object[] = [];
  // if (allClientData.length !== 0) {
  //     allClientData[0].map((a: any) => {
  //         let data = {
  //             label: a?.clientName + " (" + a.city + "/" + a.state + ")",
  //             value: {
  //                 clientId: a?.clientId,
  //                 clientName: a?.clientName,
  //                 endClientName: a?.endClientName,
  //                 MSPName: a?.mspName,
  //                 line1: a?.line1,
  //                 line2: a?.line2,
  //                 city: a?.city,
  //                 state: a?.state,
  //                 zipCode: a?.zipCode,
  //                 country: a?.country
  //             }
  //         }
  //         allClientName.push(data);
  //     });
  // }
  // const currentVendorData = useAppSelector((state: RootState) => state.vendor.vendorData);
  // const allVendorData = useAppSelector((state: RootState) => state.vendor.allVendorData);
  // let allVendorName: object[] = [];
  // if (allVendorData.length !== 0) {
  //     allVendorData[0].map((
  //         a: {
  //             vendorId: number, companyName: string, federalId: string, contactPerson: string, companyEmailID: string,
  //             contactNo: string, faxNo: string, signAuthority: string, signAuthorityDesignation: string,
  //             stateOfIncorporation: string, line1: string, line2: string, city: string, zipCode: string,
  //             state: string, country: string,
  //         }
  //     ) => {
  //         let data = {
  //             label: a.companyName,
  //             value: {
  //                 id: a.vendorId,
  //                 companyName: a.companyName,
  //                 federalId: a.federalId,
  //                 contactPerson: a.contactPerson,
  //                 companyEmailID: a.companyEmailID,
  //                 contactNo: a.contactNo,
  //                 faxNo: a.faxNo,
  //                 signAuthority: a.signAuthority,
  //                 signAuthorityDesignation: a.signAuthorityDesignation,
  //                 stateOfIncorporation: a.stateOfIncorporation,
  //                 line1: a.line1,
  //                 line2: a.line2,
  //                 city: a.city,
  //                 zipCode: a.zipCode,
  //                 state: a.state,
  //                 country: a.country,
  //             }
  //         }
  //         allVendorName.push(data);
  //     });
  // }
  // const currentJobData = useAppSelector((state: RootState) => state.job.jobData);
  // const allJobData = useAppSelector((state: RootState) => state.job.allJobData);
  // let allJobName: object[] = [];
  // if (allJobData.length !== 0) {
  //     allJobData.map((
  //         a: { id: number, requestID: number, jobDivaID: number, jobTitle: string, jobType: string, lineOfBusiness: string, jobDescription: string }
  //     ) => {
  //         let data = {
  //             label: a.jobTitle,
  //             value: {
  //                 id: a.id,
  //                 requestID: a.requestID,
  //                 jobDivaID: a.jobDivaID,
  //                 jobTitle: a.jobTitle,
  //                 jobType: a.jobType,
  //                 lineOfBusiness: a.lineOfBusiness,
  //                 jobDescription: a.jobDescription,
  //             }
  //         }
  //         allJobName.push(data);
  //     });
  // }
  // const locationName = LocationName;
  // const workAuthorization = WorkAuthorization;
  // const contractType = ContractType;
  // const workType = WorkType;
  // const jobType = JobType;
  // const resumeSource = ResumeSource;
  // const lineOfBusiness = LineOfBusiness;

  // const onValueChange = (key: any, value: any) => {
  //     dispatch(setCandidateInputBoxValue(key, value));
  // };

  // const onClientValueChange = (key: any, value: any) => {
  //     dispatch(setClientInputBoxValue(key, value));
  // };

  // const onVendorValueChange = (key: any, value: any) => {
  //     dispatch(setVendorInputBoxValue(key, value));
  // };

  // const onJobValueChange = (key: any, value: any) => {
  //     dispatch(setJobInputBoxValue(key, value));
  // };

  // function displayClientData(value: any) {
  //     onClientValueChange("id", value.clientId);
  //     onClientValueChange("endClientName", value.endClientName);
  //     onClientValueChange("mspName", value.MSPName);
  //     onClientValueChange("line1", value.line1);
  //     onClientValueChange("line2", value.line2);
  //     onClientValueChange("city", value.city);
  //     onClientValueChange("state", { label: value.state, value: value.state });
  //     onClientValueChange("zipCode", value.zipCode);
  //     onClientValueChange("country", value.country);
  // }

  // function displayVendorData(value: any) {
  //     onVendorValueChange("id", value.id);
  //     onVendorValueChange("federalID", value.federalId);
  //     onVendorValueChange("contactPerson", value.contactPerson);
  //     onVendorValueChange("companyEmailID", value.companyEmailID);
  //     onVendorValueChange("contactNo", value.contactNo);
  //     onVendorValueChange("faxNo", value.faxNo);
  //     onVendorValueChange("signAuthority", value.signAuthority);
  //     onVendorValueChange("signAuthorityDesignation", value.signAuthorityDesignation);
  //     onVendorValueChange("stateOfIncorporation", value.stateOfIncorporation);
  //     onVendorValueChange("line1", value.line1);
  //     onVendorValueChange("line2", value.line2);
  //     onVendorValueChange("city", value.city);
  //     onVendorValueChange("zipCode", value.zipCode);
  //     onVendorValueChange("state", { label: value.state, value: value.state });
  //     onVendorValueChange("country", value.country);
  // }

  // function displayJobData(value: any) {
  //     onJobValueChange("id", value.id);
  //     onJobValueChange("requestID", value.requestID);
  //     onJobValueChange("jobDivaID", value.jobDivaID);
  //     // onJobValueChange("jobTitle", value.jobTitle);
  //     onJobValueChange("jobType", { label: value.jobType, value: value.jobType });
  //     onJobValueChange("lineOfBusiness", { label: value.lineOfBusiness, value: value.lineOfBusiness });
  //     onJobValueChange("jobDescription", value.jobDescription);
  //     onJobValueChange("zipCode", value.zipCode);
  //     onJobValueChange("country", value.country);
  // }

  return (
    <>
      <CandidateDetails />

      <ClientDetails />

      <VendorDetails />
      <ReferralDetails />

      <JobDetails />
    </>
  );
};

export default BasicDetails;
