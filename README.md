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
            <h2 className=" text-center mt-9">Referral details</h2>
            <div>
                {/* <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td className="px-6 py-0">
            <Select
              options={yesNoList}
              value={currentReferralData?.Referraldetails}
              getOptionLabel={(option) => option.label}
              getOptionValue={(option) => option.value}
              onChange={(e: any) => {
                onValueChange("Referraldetails", e);
              }}
              isSearchable={true}
            />
          </td>
        </tr> */}
            </div>
            <div className="flex gap-5 " style={{ margin: "auto", width: "100%" }}>
                <div className="relative overflow-x-auto w-[100%] mt-10 border border-solid">
                    <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                        <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
                            <tr>
                                <th scope="col" className="px-6 py-3">
                                    Referral company name
                                </th>
                                <th scope="col" className="px-6 py-3">
                                    <TextField
                                        value={currentReferralData?.companyName}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("companyName", event?.target?.value);
                                        }}
                                        className=""
                                    />
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral federal ID</td>
                                <TextField
                                    value={currentReferralData?.federalID}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("federalID", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Name of contact person</td>
                                <TextField
                                    value={currentReferralData?.contactPerson}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("contactPerson", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral company email ID</td>
                                <TextField
                                    value={currentReferralData?.companyEmailID}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("companyEmailID", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral company contact no.</td>
                                <TextField
                                    value={currentReferralData?.contactNo}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("contactNo", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral fax no.</td>
                                <TextField
                                    value={currentReferralData?.faxNo}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("faxNo", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Name of sign authority</td>
                                <TextField
                                    value={currentReferralData?.signAuthority}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("signAuthority", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Designation of sign authority</td>
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
                                />
                            </tr>
                        </tbody>
                    </table>
                </div>

                <div className="relative overflow-x-auto w-[100%] mt-10 border border-solid">
                    <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                        <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"></thead>
                        <tbody>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral address line 1</td>
                                <TextField
                                    value={currentReferralData?.line1}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("line1", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral address line 2</td>
                                <TextField
                                    value={currentReferralData?.line2}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("line2", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral city</td>
                                <TextField
                                    value={currentReferralData?.city}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("city", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral Zip Code</td>
                                <TextField
                                    value={currentReferralData?.zipCode}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("zipCode", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral state</td>
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
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Country</td>
                                <TextField
                                    value={currentReferralData?.country}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("country", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                            <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4">Referral state of incorporation</td>
                                <TextField
                                    value={currentReferralData?.stateOfIncorporation}
                                    placeholder={""}
                                    handleChange={(event) => {
                                        onValueChange("stateOfIncorporation", event?.target?.value);
                                    }}
                                    className=""
                                />
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </>
    );
};

export default ReferralDetails;
