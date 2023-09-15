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



const BasicDetails: React.FC = () => {


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
