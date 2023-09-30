// chetan patil - [21/07/2023] - Start End Operations Page

import { ChangeEvent, useState } from "react";
import { TextField } from "../../common/TextField/TextField";
import { TextArea } from "../../common/TextArea/TextArea";
import "./StartEndOperations.css";
import { DropDown } from "../../common/DropDown/DropDown";
import {
    EndReasonList,
    ExitClearanceList,
    FFInvoiceStatusList,
    JobLevelList,
    JoiningStatusList,
    JoiningTypeList,
    yesNoList,
} from "../../constants/constants";
import { FloatLabel } from "../../common/FloatLabel/FloatLabel";
import Grid from "@mui/material/Unstable_Grid2";
import { Button } from "../../common/Button/Button";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import { setStartEndInputBoxValue } from "../../actions/startendoperations";
import Select from "react-select";

export const StartEndOperations: React.FC = () => {
    const dispatch = useAppDispatch();
    const currentStartEndOperationsData = useAppSelector(
        (state: RootState) => state.startEndOperations.startEndOperationsData
    );

    const onValueChange = (key: any, value: any) => {
        dispatch(setStartEndInputBoxValue(key, value));
    };

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

                <Grid xs={6} md={12}>
                   
                </Grid>

                <Grid xs={6} md={12}>
                    
                </Grid>


            </Grid> */}
            Start End operations details
            <div className="flex gap-5 " style={{ margin: "auto", width: "100%" }}>
                <div className="relative w-[100%] mt-10 ">
                <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                        <thead className='text-xs text-gray-700 uppercase bg-gray-200 dark:bg-gray-700 dark:text-gray-400'>
                        <tr>
                                <th scope="col" className="px-6 py-4">
                                    Initial details
                                </th>
                                <th></th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Recruiter name</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.recruiter}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("recruiter", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Team lead name</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.teamLead}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("teamLead", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>CRM</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.crm}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("crm", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Team manager</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.teamManager}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("teamManager", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Senior manager</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.seniorManager}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("seniorManager", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Associate director</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.assoDirector}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("assoDirector", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Center head</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.centerHead}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("centerHead", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Onsite account director</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.onsiteAccDirector}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("onsiteAccDirector", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Onboarding coordinator</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.onboCoordinator}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("onboCoordinator", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>End date</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.endDate}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("endDate", event?.target?.value);
                                        }}
                                        type="date"
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Gross BR</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.grossBr}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("grossBr", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>MSP fee in percentage</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.mspFeePercentage}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("mspFeePercentage", event?.target?.value);
                                        }}
                                    styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>MSP fee</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.mspFee}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("mspFee", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Pay rate</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.payRate}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("payRate", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Referral fee</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.refFee}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("refFee", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Tax OH percentage</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.taxOHPercentage}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("taxOHPercentage", event?.target?.value);
                                        }}
                                        styles={{ border:"1px solid hsl(0, 0%, 80%)"}}
                                    />
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
                <div className="relative w-[100%] mt-10 ">
                    <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                    <thead className='text-xs text-gray-700 uppercase bg-gray-200 dark:bg-gray-700 dark:text-gray-400'>
                            <tr>
                                <th scope="col" className="px-6 py-4">
                                    Other details
                                </th>
                                <th></th>
                            </tr>
                        </thead>
                        <tbody className="">
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Tax OH</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.taxOH}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("taxOH", event?.target?.value);
                                        }}
                                        styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Opted for health benefits</span>
                                </td>
                                <td className="px-6 py-0">
                                    <Select
                                        options={yesNoList}
                                        value={currentStartEndOperationsData.hBenefitesOpted}
                                        getOptionLabel={(option) => option.label}
                                        getOptionValue={(option) => option.value}
                                        onChange={(e: any) => {
                                            onValueChange("hBenefitesOpted", e);
                                        }}
                                        isSearchable={true}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Health benefits cost</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.hBenefitesCost}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("hBenefitesCost", event?.target?.value);
                                        }}
                                        styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Net bill rate</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.netBillRate}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("netBillRate", event?.target?.value);
                                        }}
                                        styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Net purchase</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.netPurchase}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("netPurchase", event?.target?.value);
                                        }}
                                        styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Margin</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.margin}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("margin", event?.target?.value);
                                        }}
                                        styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Full time salary offered</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        value={currentStartEndOperationsData.fullTimeSalaryOffered}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange(
                                                "fullTimeSalaryOffered",
                                                event?.target?.value
                                            );
                                        }}
                                        styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Joining status</span>
                                </td>
                                <td className="px-6 py-0">
                                    <Select
                                        options={JoiningStatusList}
                                        value={currentStartEndOperationsData.joiningStatus}
                                        getOptionLabel={(option) => option.label}
                                        getOptionValue={(option) => option.value}
                                        onChange={(e: any) => {
                                            onValueChange("joiningStatus", e);
                                        }}
                                        isSearchable={true}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Joining type</span>
                                </td>
                                <td className="px-6 py-0">
                                    <Select
                                        options={JoiningTypeList}
                                        value={currentStartEndOperationsData.joiningType}
                                        getOptionLabel={(option) => option.label}
                                        getOptionValue={(option) => option.value}
                                        onChange={(e: any) => {
                                            onValueChange("joiningType", e);
                                        }}
                                        isSearchable={true}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Exit clearance type</span>
                                </td>
                                <td className="px-6 py-0">
                                    <Select
                                        options={ExitClearanceList}
                                        value={currentStartEndOperationsData.exitClearance}
                                        getOptionLabel={(option) => option.label}
                                        getOptionValue={(option) => option.value}
                                        onChange={(e: any) => {
                                            onValueChange("exitClearance", e);
                                        }}
                                        isSearchable={true}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>End reason type</span>
                                </td>
                                <td className="px-6 py-0">
                                    <Select
                                        options={EndReasonList}
                                        value={currentStartEndOperationsData.endReason}
                                        getOptionLabel={(option) => option.label}
                                        getOptionValue={(option) => option.value}
                                        onChange={(e: any) => {
                                            onValueChange("endReason", e);
                                        }}
                                        isSearchable={true}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Job level</span>
                                </td>
                                <td className="px-6 py-0">
                                    <Select
                                        options={JobLevelList}
                                        value={currentStartEndOperationsData.jobLevel}
                                        getOptionLabel={(option) => option.label}
                                        getOptionValue={(option) => option.value}
                                        onChange={(e: any) => {
                                            onValueChange("jobLevel", e);
                                        }}
                                        isSearchable={true}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Select FF invoice status</span>
                                </td>
                                <td className="px-6 py-0">
                                    <Select
                                        options={FFInvoiceStatusList}
                                        value={currentStartEndOperationsData.ffInvoiceStatus}
                                        getOptionLabel={(option) => option.label}
                                        getOptionValue={(option) => option.value}
                                        onChange={(e: any) => {
                                            onValueChange("ffInvoiceStatus", e);
                                        }}
                                        isSearchable={true}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>Joining status remarks</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        // className="start-end-textarea"
                                        // label="Joining Status Remarks"
                                        value={currentStartEndOperationsData.joiningStatusRemark}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange(
                                                "joiningStatusRemark",
                                                event?.target?.value
                                            );
                                        }}
                                        styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                                    />
                                </td>
                            </tr>
                            <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                                <td className="px-6 py-4 font-semibold">
                                    <span>End remarks</span>
                                </td>
                                <td className="px-6 py-0">
                                    <TextField
                                        // className="start-end-textarea"
                                        // label="End Remarks"
                                        value={currentStartEndOperationsData.endRemarks}
                                        placeholder={""}
                                        handleChange={(event) => {
                                            onValueChange("endRemarks", event?.target?.value);
                                        }}
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
