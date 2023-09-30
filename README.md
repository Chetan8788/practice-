import React from "react";
import Grid from "@mui/material/Unstable_Grid2";
import { TextField } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import { setVendorInputBoxValue } from "../../actions/vendor";
import { LocationName } from "../../constants/candidateclientconstants";
import Select from "react-select";

const VendorDetails: React.FC = () => {
  const dispatch = useAppDispatch();
  const currentVendorData = useAppSelector(
    (state: RootState) => state.vendor.vendorData
  );
  const allVendorData = useAppSelector(
    (state: RootState) => state.vendor.allVendorData
  );
  let allVendorName: object[] = [];
  if (allVendorData.length !== 0) {
    allVendorData.map((a: any) => {
      a?.addressId.map((b: any) => {
        let data = {
          label: a.vendorId.companyName,
          value: {
            id: a.vendorId.id,
            companyName: a.vendorId.companyName,
            federalId: a.vendorId.federalId,
            contactPerson: a.vendorId.contactPerson,
            email: b?.contactDetailId?.email,
            contactNumber: b?.contactDetailId?.contactNumber,
            faxNumber: b?.contactDetailId?.faxNumber,
            signAuthority: a.vendorId.signAuthority,
            signAuthorityDesignation: a.vendorId.signAuthorityDesignation,
            stateOfIncorporation: a.vendorId.stateOfIncorporation,
            line1: b.line1,
            line2: b.line2,
            city: b.city,
            zipCode: b.zipCode,
            state: b.state,
            country: b.country,
          },
        };
        allVendorName.push(data);
      });
    });
  }
  const locationName = LocationName;

  const onVendorValueChange = (key: any, value: any) => {
    dispatch(setVendorInputBoxValue(key, value));
  };

  function displayVendorData(value: any) {
    onVendorValueChange("id", value.id);
    onVendorValueChange("federalID", value.federalId);
    onVendorValueChange("contactPerson", value.contactPerson);
    onVendorValueChange("email", value.email);
    onVendorValueChange("contactNumber", value.contactNumber);
    onVendorValueChange("faxNumber", value.contactNumber);
    onVendorValueChange("signAuthority", value.signAuthority);
    onVendorValueChange(
      "signAuthorityDesignation",
      value.signAuthorityDesignation
    );
    onVendorValueChange("stateOfIncorporation", value.stateOfIncorporation);
    onVendorValueChange("line1", value.line1);
    onVendorValueChange("line2", value.line2);
    onVendorValueChange("city", value.city);
    onVendorValueChange("zipCode", value.zipCode);
    onVendorValueChange("state", { label: value.state, value: value.state });
    onVendorValueChange("country", value.country);
  }

  return (
    <>
      <h1 className="mt-7">Vendor details</h1>
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
                  <span>Vendore Details</span>
                </td>

                <th scope="col" className="px-6 py-0">
                  <Select
                    options={allVendorName}
                    value={currentVendorData?.companyName}
                    getOptionLabel={(option) => option.label}
                    getOptionValue={(option) => option.value}
                    onChange={(e: any) => {
                      displayVendorData(e.value);
                      onVendorValueChange("companyName", e);
                    }}
                    isSearchable={true}
                    styles={{
                      control: (baseStyles, state) => ({
                        ...baseStyles,
                        backgroundColor: "rgb(249 250 251)",
                      }),
                    }}
                  />
                </th>
              </tr>

              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Vendore Federal Id</span>
                </td>{" "}
                <td className="px-6 py-4">{currentVendorData?.federalID}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Name Of Contact Person</span>
                </td>{" "}
                <td className="px-6 py-4">
                  {currentVendorData?.contactPerson}
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Vendor Company Email</span>
                </td>{" "}
                <td className="px-6 py-4">{currentVendorData?.email}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Vendore Company Contact Number</span>
                </td>{" "}
                <td className="px-6 py-4">
                  {currentVendorData?.contactNumber}
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Vendore Fax No</span>
                </td>{" "}
                <td className="px-6 py-4">{currentVendorData?.faxNumber}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Name Of Sign Authority</span>
                </td>{" "}
                <td className="px-6 py-4">
                  {currentVendorData?.signAuthority}
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Designation of sign authority</span>
                </td>
                <td className="px-6 py-4">
                  {currentVendorData?.signAuthorityDesignation}
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
                  <span>Vendor state of incorporation</span>
                </td>
                <td className="px-6 py-4">
                  {currentVendorData?.stateOfIncorporation}
                </td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Line 1</span>
                </td>
                <td className="px-6 py-4">{currentVendorData?.line1}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Line 2</span>
                </td>
                <td className="px-6 py-4">{currentVendorData?.line2}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>City</span>
                </td>
                <td className="px-6 py-4">{currentVendorData?.city}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Zip Code</span>
                </td>
                <td className="px-6 py-4">{currentVendorData?.zipCode}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>State</span>
                </td>
                <td className="px-6 py-4">{currentVendorData?.state.value}</td>
              </tr>
              <tr className="bg-[#f8f8f8dd] border-b dark:bg-gray-800 dark:border-gray-700">
                <td className="px-6 py-4 font-semibold">
                  <span>Country</span>
                </td>
                <td className="px-6 py-4">{currentVendorData?.country}</td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </>
  );
};

export default VendorDetails;
