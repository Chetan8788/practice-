import React, { ChangeEvent, useState } from "react";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import { setReferralInputBoxValue } from "../../actions/referral";
import { DropDown } from "../../common/DropDown/DropDown";
import { LocationName } from "../../constants/candidateclientconstants";
import { yesNoList } from "../../constants/constants";
import Select from "react-select";

const ReferralDetails: React.FC = () => {
  const dispatch = useAppDispatch();
  const currentReferralData = useAppSelector(
    (state: RootState) => state.referral.referralData
  );
  const locationName = LocationName;

  const onValueChange = (key: any, value: any) => {
    dispatch(setReferralInputBoxValue(key, value));
  };

  return (
    <>
      Referral details
      <div className="flex gap-5 " style={{ margin: "auto", width: "100%" }}>
        <div className="relative w-[100%] mt-10 ">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-200 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" className="px-6 py-4">
                  Initial details
                </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold ">
                  <span> Referral company name</span>
                </td>

                <th scope="col" className="px-6 py-3">
                  <TextField
                    value={currentReferralData?.companyName}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("companyName", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </th>
              </tr>

              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral Fedaral Id</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.federalID}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("federalID", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Name Of Contact Person</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.contactPerson}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("contactPerson", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral Company Email Id</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.companyEmailID}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("companyEmailID", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral Company Contact No</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.contactNo}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("contactNo", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral Fax No</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.faxNo}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("faxNo", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Name Of Sign Authority</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.signAuthority}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("signAuthority", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Designation of sign authority</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.signAuthorityDesignation}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange(
                        "signAuthorityDesignation",
                        event?.target?.value
                      );
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>

        <div className="relative w-[100%] mt-10 bg-[#f8f8f8dd]">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-200 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" className="px-6 py-4">
                  Other details
                </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral address line 1</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.line1}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("line1", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral address line 2</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.line2}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("line2", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral City</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.city}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("city", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral Zip Code</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.zipCode}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("zipCode", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral State</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={locationName}
                    value={currentReferralData?.state}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("state", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Country</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.country}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("country", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral State Incorporation</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentReferralData?.stateOfIncorporation}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange(
                        "stateOfIncorporation",
                        event?.target?.value
                      );
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </>
  );
};

export default ReferralDetails;
