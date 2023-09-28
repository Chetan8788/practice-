import React, { useEffect, useState } from "react";
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
import { yesNoList } from "../../constants/constants";
import { DropDown } from "../../common/DropDown/DropDown";

const BasicDetails: React.FC = () => {
  const [flag, setFlag] = useState<boolean>(false);
  const [selectedOption, setSelectedOption] = useState<any>();
  console.log("selectedOption::::", selectedOption);
  console.log("flag:::", flag);

  function select(e: any) {
    setSelectedOption(e);
    if (selectedOption?.includes("Yes")) {
      setFlag(true);
    }
    // else if (selectedOption.includes("No")) {
    //   setFlag(false);
    // }
  }

  return (
    <>
      <CandidateDetails />
      <ClientDetails />
      <VendorDetails />

      <div className="w-[30%] mt-10">
        <span className="text-left ml-[-45%] text-sm">
          Do you want to add a referral ?
        </span>
        <Select
          className="mt-2"
          options={yesNoList}
          value={selectedOption?.value}
          getOptionLabel={(option) => option.label}
          getOptionValue={(option) => option.value}
          onChange={(e: any) => {
            select(e.value);
          }}
          isSearchable={true}
        />
      </div>

      {selectedOption === "Yes" && <ReferralDetails />}
      <JobDetails />
    </>
  );
};

export default BasicDetails;
