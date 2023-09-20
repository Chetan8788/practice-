import React, { useEffect, useState } from "react";
import ContentAreaScreen from "../ContentArea";
import SideBarScreen from "../Sidebar";
import NavBarScreen from "../Navbar";
import MiniDrawer from "./Homepage";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import { RootState } from "../../redux/store";
import {
  allCandidateData,
  getCandidate,
  getImportantCandidateData,
} from "../../actions/candidate";
import { useNavigate } from "react-router-dom";
import DeleteForeverIcon from "@mui/icons-material/DeleteForever";
import Button from "@mui/material/Button";
import { Link } from "react-router-dom";
import { getCandidateBackgroundCheck } from "../../actions/backgroundCheck";
import { getCandidateDocumentation } from "../../actions/documentation";
import { getCandidateStartEndOperations } from "../../actions/startendoperations";
import { getCandidateRateRevision } from "../../actions/raterevision";

const HomepageScreen: React.FC = () => {
  const navigate = useNavigate();
  const dispatch = useAppDispatch();

  useEffect(() => {
    dispatch(allCandidateData());
  }, []);

  let candidateData: any = useAppSelector(
    (state: RootState) => state.candidate.getAllCandidates
  );
  let candidateDataRow = candidateData;
  console.log("candidateDataRow: ", candidateDataRow);
  const [open, setOpen] = useState(false);
  const [singleCandidateData, setSingleCandidateData] = useState({});
  const [filteredData, setFilteredData] = useState<any>();
  console.log("filteredData", filteredData);
  const [count, setCount] = useState(true);

  useEffect(() => {
    setFilteredData(candidateData);
    if (count) {
      if (candidateData?.length !== 0) {
        setFilteredData(
          candidateData?.filter((cd: { candidateId: any }) =>
            cd?.candidateId?.firstName?.toLowerCase()?.includes("")
          )
        );
        setCount(false);
      }
    }
  }, [candidateData]);

  const filterResult = (event: any) => {
    // debugger;
    setFilteredData(candidateDataRow);
    let value: string = event.target.value;

    if (candidateData?.length !== 0) {
      setFilteredData(
        candidateData?.filter((cd: { candidateId: any }) =>
          cd?.candidateId?.firstName
            ?.toLowerCase()
            ?.includes(value.toLowerCase())
        )
      );
    }
  };

  const showCandidate = (data: any) => {
    setSingleCandidateData(data);
    setOpen(true);
  };

  function deleteJob(id: any): void {
    // dispatch(deleteCandidateData(id));
    // setCount(true);
  }

  const boxStyle = {
    alignItems: "center",
    border: "none",
    flexGrow: 1,
    marginTop: "3%",
    overflowY: "auto",
    overflowX: "hidden",
    height: "60vh",
    paddingRight: "10px",
    paddingLeft: "10px",
  };

  const button = {
    backgroundColor: "Green",
    border: "none",
    color: "white",
    padding: "15px 32px",
    textAlign: "center",
    textDecoration: "none",
    display: "inline - block",
    fontSize: "16px",
  };
  ////////////////////////////// bhushan work/////////////// sort by ace and desc order///
  const [data3, setData3] = useState<any>();
  const [flag, setFlag] = useState<boolean>(false);
  const [isAscending, setIsAscending] = useState(true);

  console.log("data3", data3);

  function sorting() {
    setIsAscending((prevIsAscending) => !prevIsAscending);

    if (!flag) {
      setData3(
        filteredData.sort((a: any, b: any) =>
          a?.candidateId.firstName?.localeCompare(b?.candidateId.firstName)
        )
      );
      setFlag(true);
    } else {
      setData3(
        filteredData.sort((a: any, b: any) =>
          b?.candidateId.firstName?.localeCompare(a?.candidateId.firstName)
        )
      );
      setFlag(false);
    }
  }
  return (
    <>
      <div style={{ display: "flex" }}>
        <div
          style={{ borderRadius: "15px", marginBottom: "10px", width: "90%" }}
          className="py-3 px-4"
        >
          <div className="relative max-w">
            <label htmlFor="hs-table-search" className="sr-only">
              Search
            </label>
            <Button
              onClick={sorting}
              style={{
                border: "1px solid",
                backgroundColor: "#1976d2",
                color: "white",
              }}
            >
              {" "}
              short {isAscending ? "Descending" : "Ascending"}
            </Button>

            <input
              style={{ border: "0.5px solid gray" }}
              type="text"
              name="hs-table-search"
              id="hs-table-search"
              className="ml-[-13px] p-2 mt-[-40px] pl-10 block w-[35%] border-gray-200 rounded-md text-sm focus:border-blue-500 focus:ring-blue-500 dark:bg-slate-900 dark:border-gray-700 dark:text-gray-400"
              placeholder="Search for candidates"
              onChange={(event) => filterResult(event)}
            />
            <div className="absolute inset-y-0 left-0 flex items-center pointer-events-none pl-2">
              <svg
                className="h-3.5 w-3.5 text-gray-400"
                xmlns="http://www.w3.org/2000/svg"
                width="16"
                height="16"
                fill="currentColor"
                viewBox="0 0 16 16"
              >
                <path d="M11.742 10.344a6.5 6.5 0 1 0-1.397 1.398h-.001c.03.04.062.078.098.115l3.85 3.85a1 1 0 0 0 1.415-1.414l-3.85-3.85a1.007 1.007 0 0 0-.115-.1zM12 6.5a5.5 5.5 0 1 1-11 0 5.5 5.5 0 0 1 11 0z" />
              </svg>
            </div>
          </div>
        </div>
      </div>
      <div className="flex flex-col" style={{ height: "70vh" }}>
        <div className="-m-1.5 overflow-x-auto">
          <div className="p-1.5 min-w-full inline-block align-middle">
            <div className="border rounded-lg divide-y divide-gray-200 dark:border-gray-700 dark:divide-gray-700">
              {/* ///////////////////////////bhushan work///////////////////////// */}

              <div className="relative overflow-x-auto shadow-md sm:rounded-lg">
                <table className="w-full text-sm text-left text-gray-500 dark:text-gray-400">
                  <thead className="text-xs text-white divide-y uppercase bg-[#1976d2] border-solid border-2 ">
                    <tr>
                      <th
                        scope="col"
                        className="px-6 py-3 border border-slate-300 text-center"
                      >
                        candidate name
                      </th>
                      <th
                        scope="col"
                        className="px-6 py-3 border border-slate-300 text-center"
                      >
                        worktype
                      </th>
                      <th
                        scope="col"
                        className="px-6 py-3 border border-slate-300 text-center"
                      >
                        address
                      </th>
                      <th
                        scope="col"
                        className="px-6 py-3 border border-slate-300 text-center"
                      >
                        contactNumber
                      </th>
                      <th
                        scope="col"
                        className="px-6 py-3 border border-slate-300 text-center"
                      >
                        email
                      </th>
                      <th
                        scope="col"
                        className="px-6 py-3 border border-slate-300 text-center"
                      >
                        action
                      </th>
                      <th
                        scope="col"
                        className="px-6 py-3 border border-slate-300 text-center"
                      >
                        action
                      </th>
                    </tr>
                  </thead>
                  <tbody className="">
                    {!flag
                      ? filteredData?.map((ele: any, index: any) => (
                          <tr>
                            <td className="border-b p-5 ml-3 border border-slate-300 text-center">
                              {ele.candidateId.firstName +
                                " " +
                                ele.candidateId.lastName}
                            </td>
                            <td className="border-b p-5 ml-3 border border-slate-300 text-center">
                              {ele.candidateId.workType}
                            </td>
                            <td className="border-b p-5 ml-3 border border-slate-300 text-center">
                              {ele.addressId[0].city +
                                " " +
                                ele.addressId[0].state}
                            </td>
                            <td className="border-b p-5 ml-3 border border-slate-300 text-center">
                              {ele.addressId[0].contactDetailId.contactNumber}
                            </td>
                            <td className="border-b p-5 ml-3 border border-slate-300 text-center">
                              {ele.addressId[0].contactDetailId.email}
                            </td>

                            <td className="border-b border border-slate-300 text-center border-solid">
                              <Button className=""> Delete</Button>
                            </td>
                            <td className="border-b border border-slate-300 text-center">
                              <Button className=""> Edit</Button>
                            </td>
                          </tr>
                        ))
                      : data3?.map((ele: any, index: any) => (
                          <tr>
                            <td className="border-b p-5 ml-3 border border-slate-300 text-center">
                              {ele.candidateId.firstName +
                                " " +
                                ele.candidateId.lastName}
                            </td>
                            <td className="border-b border border-slate-300 text-center">
                              {ele.candidateId.workType}
                            </td>
                            <td className="border-b border border-slate-300 text-center">
                              {ele.addressId[0].city +
                                " " +
                                ele.addressId[0].state}
                            </td>
                            <td className="border-b border border-slate-300 text-center">
                              {ele.addressId[0].contactDetailId.contactNumber}
                            </td>
                            <td className="border-b border border-slate-300 text-center">
                              {ele.addressId[0].contactDetailId.email}
                            </td>

                            <td className="border-b border border-slate-300 text-center">
                              <Button className=""> Delete</Button>
                            </td>
                            <td className="border-b border border-slate-300 text-center">
                              <Button className=""> Edit</Button>
                            </td>
                          </tr>
                        ))}
                  </tbody>
                </table>
              </div>
            </div>
          </div>
        </div>
      </div>
      {/* <ShowJob open={open} setOpen={setOpen} data={singleJobData} showTableCount={setCount} /> */}
    </>
  );
};

export default HomepageScreen;

