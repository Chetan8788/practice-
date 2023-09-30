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

  return (
    <>
      Rate revision details
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
                <td className="px-6 py-4 font-semibold">
                  <span>Gross BR</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.grossBr}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("grossBr", event?.target?.value);
                    }}
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                    // className="rate-revision-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>MSP fee in percentage</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.mspFeePercentage}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("mspFeePercentage", event?.target?.value);
                    }}
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>MSP fee</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.mspFee}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("mspFee", event?.target?.value);
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
                    value={currentRateRevisionData?.netBillRate}
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
                  <span>Pay rate</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.payRate}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("payRate", event?.target?.value);
                    }}
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Referral fee</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.refFee}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("refFee", event?.target?.value);
                    }}
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Tax OH percentage</span>
                </td>
                <td className="px-6 py-0 ">
                  <TextField
                    value={currentRateRevisionData?.taxOHPercentage}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("taxOHPercentage", event?.target?.value);
                    }}
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div className="relative w-[100%] mt-10 ">
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
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Tax OH</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.taxOH}
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
                  <span>Health benefits cost</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentRateRevisionData?.healthB}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("healthB", event?.target?.value);
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
                    value={currentRateRevisionData?.netPurchase}
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
                    value={currentRateRevisionData?.margin}
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
                  <span>Rate revision reason</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    // className="rate-revision-textarea"
                    value={currentRateRevisionData?.rateRevisionReason}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange("rateRevisionReason", event?.target?.value);
                    }}
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
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
