import React, { ChangeEvent, useState } from "react";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { TextArea } from "../../common/TextArea/TextArea";
import { setJobInputBoxValue } from "../../actions/job";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import Select from "react-select";
import {
  JobTypeList,
  LineOfBusinessList,
  ResumeSourceList,
  WorkTypeList,
} from "../../constants/jobconstants";

const JobDetails: React.FC = () => {
  const dispatch = useAppDispatch();
  const currentJobData = useAppSelector(
    (state: RootState) => state.job.jobData
  );
  const allJobData = useAppSelector((state: RootState) => state.job.allJobData);
  let allJobName: object[] = [];
  if (allJobData.length !== 0) {
    allJobData.map(
      (a: {
        id: number;
        requestID: number;
        jobDivaID: number;
        jobTitle: string;
        jobType: string;
        lineOfBusiness: string;
        jobDescription: string;
      }) => {
        let data = {
          label: a.jobTitle,
          value: {
            id: a.id,
            requestID: a.requestID,
            jobDivaID: a.jobDivaID,
            jobTitle: a.jobTitle,
            jobType: a.jobType,
            lineOfBusiness: a.lineOfBusiness,
            jobDescription: a.jobDescription,
          },
        };
        allJobName.push(data);
      }
    );
  }
  const workType = WorkTypeList;
  const jobType = JobTypeList;
  const resumeSource = ResumeSourceList;
  const lineOfBusiness = LineOfBusinessList;

  const onJobValueChange = (key: any, value: any) => {
    dispatch(setJobInputBoxValue(key, value));
  };

  function displayJobData(value: any) {
    onJobValueChange("id", value.id);
    onJobValueChange("requestID", value.requestID);
    onJobValueChange("jobDivaID", value.jobDivaID);
    // onJobValueChange("jobTitle", value.jobTitle);
    onJobValueChange("jobType", { label: value.jobType, value: value.jobType });
    onJobValueChange("lineOfBusiness", {
      label: value.lineOfBusiness,
      value: value.lineOfBusiness,
    });
    onJobValueChange("jobDescription", value.jobDescription);
    onJobValueChange("zipCode", value.zipCode);
    onJobValueChange("country", value.country);
  }

  return (
    <>
      <h1 className="mt-7">Job Details</h1>
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
                  <span> Job title/Position name</span>
                </td>
                <th scope="col" className="px-6 py-0">
                  <Select
                    options={allJobName}
                    value={currentJobData?.jobTitle}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      displayJobData(e.value);
                      onJobValueChange("jobTitle", e);
                    }}
                    isSearchable={true}
                  />
                </th>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold ">
                  <span>Working From</span>
                </td>
                <td className="px-6 py-0 ">
                  <TextField
                    value={currentJobData?.workingFrom}
                    placeholder={""}
                    handleChange={(event) => {
                      onJobValueChange("workingFrom", event?.target?.value);
                    }}
                    className=""
                    styles={{ border: "1px solid hsl(0, 0%, 80%)" }}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Work Type</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={workType}
                    value={currentJobData?.workType}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onJobValueChange("workType", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Resume Resource</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={resumeSource}
                    value={currentJobData?.resumeSource}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onJobValueChange("resumeSource", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold ">
                  <span>Skill Set</span>
                </td>
                <td className="px-6 py-0 ">
                  <TextField
                    value={currentJobData?.skillSet}
                    placeholder={""}
                    handleChange={(event) => {
                      onJobValueChange("skillSet", event?.target?.value);
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
                  <span>Request Id</span>
                </td>
                <td className="px-6 py-4">{currentJobData?.requestID}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Job Diva Id</span>
                </td>
                <td className="px-6 py-4">{currentJobData?.jobDivaID}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Job Type</span>
                </td>
                <td className="px-6 py-4">{currentJobData?.jobType.value}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Line Of Business</span>
                </td>
                <td className="px-6 py-4">
                  {currentJobData?.lineOfBusiness.value}
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Job Discription</span>
                </td>
                <td className="px-6 py-4">{currentJobData?.jobDescription}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </>
  );
};

export default JobDetails;
