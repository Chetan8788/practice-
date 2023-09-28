// Ajay Bagul - [21/07/2023] - Documentation page

import { ChangeEvent, useState } from "react";
import { TextField } from "../../common/TextField/TextField";
import { TextArea } from "../../common/TextArea/TextArea";
import "./Documentation.css";
import Grid from "@mui/material/Unstable_Grid2";
import { DropDown } from "../../common/DropDown/DropDown";
import {
  ArticlesOfIncorporationList,
  CertificateOfInsuranceList,
  CipcicaCipcicuList,
  ClientTaskOrderOrSOWList,
  ClientTaskOrderOrSOWStepList,
  ClientTaskOrderSigningList,
  DirectDepositeAgreementList,
  DocumentationStatusList,
  EVerifyList,
  EemergencyFormList,
  GoodStandingDocumentationList,
  I9FormList,
  ListADocumentsList,
  ListBDocumentsList,
  ListCDocumentsList,
  MSAList,
  SOWList,
  VaccinationStatusList,
  VoidCheckEmailList,
  W9W4List,
  WorkAuthorizeDocumentationList,
  yesNoList,
} from "../../constants/constants";
import { Button } from "../../common/Button/Button";
import { RootState } from "../../redux/store";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { setDocumentationCheckInputBoxValue } from "../../actions/documentation";
import { useDispatch } from "react-redux";
import Select from "react-select";

export const Documentation: React.FC = () => {
  const dispatch = useAppDispatch();
  const currentDocumentationData = useAppSelector(
    (state: RootState) => state?.documentation?.documentationData
  );

  // const [articlesOfIncorporation, setArticlesOfIncorporation] = useState<any>();
  // const [W9W4, setW9W4] = useState<any>();
  // const [directDepositAgreement, setDirectDepositAgreement] = useState<any>();
  // const [voidCheckEmail, setVoidCheckEmail] = useState<any>();
  // const [cipcicaCipcicu, setCipcicaCipcicu] = useState<any>();
  // const [goodStandingDocumentation, setGoodStandingDocumentation] =
  //   useState<any>();
  // const [workAuthorizeDocumentation, setWorkAuthorizeDocumentation] =
  //   useState<any>();
  // const [i9Form, setI9Form] = useState<any>();
  // const [listADocuments, setListADocuments] = useState<any>();
  // const [listBDocuments, setListBDocuments] = useState<any>();
  // const [listCDocuments, setListCDocuments] = useState<any>();
  // const [eVerify, setEVerify] = useState<any>();
  // const [eVerificationDate, setEVerificationDate] = useState<any>();
  // const [emergencyForm, setEmergencyForm] = useState<any>();
  // const [vaccinationStatus, setVaccinationStatus] = useState<any>();
  // const [MSA, setMSA] = useState<any>();
  // const [SOW, setSOW] = useState<any>();
  // const [SOWValidity, setSOWValidity] = useState<any>();
  // const [certificateOfInsurance, setCertificateOfInsurance] = useState<any>();
  // const [certificateOfInsuranceDate, setCertificateOfInsuranceDate] =
  //   useState<any>();
  // const [clientTaskOrderOrSOW, setClientTaskOrderOrSOW] = useState<any>();
  // const [clientTaskOrderOrSOWStep, setClientTaskOrderOrSOWStep] =
  //   useState<any>();
  // const [clientTaskOrderSigning, setClientTaskOrderSigning] = useState<any>();
  // const [taskOrderExpiryDate, setTaskOrderExpiryDate] = useState<any>();
  // const [documentationStatus, setDocumentationStatus] = useState<any>();
  // const [documentationRemark, setDocumentationRemark] = useState<any>();
  // const [docuCompletionDate, setDocuCompletionDate] = useState<any>();

  const onValueChange = (key: any, value: any) => {
    if (key && value) {
      dispatch(setDocumentationCheckInputBoxValue(key, value));
    }
  };

  return (
    <>
      {/* <Grid container spacing={4}>
        <Grid xs={6} md={3}>
          <span>Articles of incorporation</span>
          
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
      </Grid> */}
      Documentation details
      <div className="flex gap-5 " style={{ margin: "auto", width: "100%" }}>
        <div className="relative w-[100%] mt-10 border border-solid">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
            <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" className="px-6 py-3">
                  {/* <span>Documentation</span> */}
                </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Articles of incorporation</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={ArticlesOfIncorporationList}
                    value={
                      currentDocumentationData?.articlesOrCertificateOFIncorporation
                    }
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("articlesOrCertificateOFIncorporation", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>W9 Or W4</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={W9W4List}
                    value={currentDocumentationData?.w9Orw4}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("w9Orw4", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Direct deposit agreement</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={DirectDepositeAgreementList}
                    value={currentDocumentationData?.directDepositAgreement}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("directDepositAgreement", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Void check email</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={VoidCheckEmailList}
                    value={currentDocumentationData?.voidCheckOrEmailContent}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("voidCheckOrEmailContent", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>CIPCIA Or CIPCICU</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={CipcicaCipcicuList}
                    value={currentDocumentationData?.CIPCICICAOrCIPCICU}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("CIPCICICAOrCIPCICU", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Good standing documentation</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={GoodStandingDocumentationList}
                    value={currentDocumentationData?.goodStandingDocument}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("goodStandingDocument", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Work authorization documentation</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={WorkAuthorizeDocumentationList}
                    value={currentDocumentationData?.workAuthorizationDocument}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("workAuthorizationDocument", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>I9 Form</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={I9FormList}
                    value={currentDocumentationData?.I9Form}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("I9Form", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>List A documents</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={ListADocumentsList}
                    value={currentDocumentationData?.listADocument}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("listADocument", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>List B documents</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={ListBDocumentsList}
                    value={currentDocumentationData?.listBDocument}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("listBDocument", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>List C documents</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={ListCDocumentsList}
                    value={currentDocumentationData?.listCDocument}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("listCDocument", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>E-Verify</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={EVerifyList}
                    value={currentDocumentationData?.E_verify}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("E_verify", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>E-Verification date</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentDocumentationData?.E_verificationDate}
                    type="date"
                    handleChange={(e: any) => {
                      onValueChange("E_verificationDate", e.target.value);
                    }}
                    // className="documentation-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Emergency form</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={EemergencyFormList}
                    value={currentDocumentationData?.emergencyForm}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("emergencyForm", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
            </tbody>
          </table>
        </div>
        <div className="relative w-[100%] mt-10">
          <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400 border border-solid">
            <thead className="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
              <tr>
                <th scope="col" className="px-6 py-3">
                  {/* <span>Documentation</span> */}
                </th>
                <th></th>
              </tr>
            </thead>
            <tbody>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Vaccination status</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={VaccinationStatusList}
                    value={currentDocumentationData?.vaccinationStatus}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("vaccinationStatus", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Client task order or SOW step</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={ClientTaskOrderOrSOWStepList}
                    value={currentDocumentationData?.clientTaskOrderOrSOWst}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("clientTaskOrderOrSOWst", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>MSA</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={MSAList}
                    value={currentDocumentationData?.MSA}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("MSA", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>SOW</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={SOWList}
                    value={currentDocumentationData?.SOW}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("SOW", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>SOW Validity</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentDocumentationData?.SOWValidity}
                    type="date"
                    handleChange={(e: any) => {
                      onValueChange("SOWValidity", e.target.value);
                    }}
                    // className="documentation-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Certificate of insurance</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={CertificateOfInsuranceList}
                    value={
                      currentDocumentationData?.certificateOFInsuranceOrCOI
                    }
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("certificateOFInsuranceOrCOI", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Client task order signing</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={ClientTaskOrderSigningList}
                    value={currentDocumentationData?.clientTaskOrderSigning}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("clientTaskOrderSigning", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Task order expiry date</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentDocumentationData?.TaskOrderExpiryDate}
                    type="date"
                    handleChange={(e: any) => {
                      onValueChange("TaskOrderExpiryDate", e.target.value);
                    }}
                    // className="documentation-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Certificate of insurance date</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentDocumentationData?.certificationOfInsurance}
                    type="date"
                    handleChange={(e: any) => {
                      onValueChange("certificationOfInsurance", e.target.value);
                    }}
                    // className="documentation-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Client task order or SOW</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={ClientTaskOrderOrSOWList}
                    value={currentDocumentationData?.clientTaskOrderOrSOW}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("clientTaskOrderOrSOW", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Documentation status</span>
                </td>
                <td className="px-6 py-0">
                  <Select
                    options={DocumentationStatusList}
                    value={currentDocumentationData?.documentationStatus}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      onValueChange("documentationStatus", e);
                    }}
                    isSearchable={true}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Documents completion date</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={
                      currentDocumentationData?.documentationCompletionDate
                    }
                    type="date"
                    handleChange={(e: any) => {
                      onValueChange(
                        "documentationCompletionDate",
                        e.target.value
                      );
                    }}
                    // className="documentation-textfield"
                    // styles={{ width: "" }}
                  />
                </td>
              </tr>
              <tr className="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4">
                  <span>Documentation remarks</span>
                </td>
                <td className="px-6 py-0">
                  <TextField
                    value={currentDocumentationData?.documentationRemark}
                    placeholder={""}
                    handleChange={(event) => {
                      onValueChange(
                        "documentationRemark",
                        event?.target?.value
                      );
                    }}
                    className=""
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
