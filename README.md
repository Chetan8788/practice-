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
      <Grid xs={12} md={12}>
        <h2 style={{ marginTop: "40px" }}>Job details</h2>
      </Grid>
      <div className="flex gap-5 " style={{ margin: "auto", width: "100%" }}>
        <div className="relative overflow-x-auto w-[100%] mt-10 border border-solid">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" className="px-6 py-6 border-b">
                  Job title/Position name
                </th>
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
            </thead>
            <tbody>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Working from</td>
                <td className="px-6 py-4">
                  <TextField
                    value={currentJobData?.workingFrom}
                    placeholder={""}
                    handleChange={(event) => {
                      onJobValueChange("workingFrom", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Work type</td>
                <td className="px-6 py-4">
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
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Resume source</td>
                <td className="px-6 py-4">
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
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Skill set</td>
                <td className="px-6 py-4">
                  <TextField
                    value={currentJobData?.skillSet}
                    placeholder={""}
                    handleChange={(event) => {
                      onJobValueChange("skillSet", event?.target?.value);
                    }}
                    className=""
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div className="relative overflow-x-auto w-[100%] mt-10 border border-solid">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"></thead>
            <tbody>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Request ID</td>
                <td className="px-6 py-4">{currentJobData?.requestID}</td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Job diva ID</td>
                <td className="px-6 py-4">{currentJobData?.jobDivaID}</td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Job type</td>
                <td className="px-6 py-4">{currentJobData?.jobType.value}</td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Line of business</td>
                <td className="px-6 py-4">
                  {currentJobData?.lineOfBusiness.value}
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">Job description</td>
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
