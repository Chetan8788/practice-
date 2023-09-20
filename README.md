import { Cog6ToothIcon, DocumentIcon, EyeIcon, LinkIcon, NoSymbolIcon, PencilSquareIcon, TrashIcon } from '@heroicons/react/24/outline';
import { Bars3BottomLeftIcon, BarsArrowDownIcon, BarsArrowUpIcon } from '@heroicons/react/24/solid';

import { Typography, Tooltip, Checkbox, Avatar } from '@material-tailwind/react';
import { sortBy } from 'lodash';
import React, { useState } from 'react'
import { useEffect } from 'react';
import Pagination from './Pagination';
import moment from 'moment-timezone';

function GenericTable({onSelectCheckbox, showAvatar = false, onPressAction, onPressSort, tableHeader = [], tableData: tableBody = [], actionType = [], showCheckbox = false, sortValue, loading = false, onPageChange, count = 0, showColumnLink = [], onClickRow }) {
  const [sort, setSort] = useState(undefined);
  // const [photoUploading, setPhotoUploading] = useState(false);
  const [selectedCheckboxIds, setSelectedCheckboxIds] = useState([]);

  const [tableData, setTableData] = useState(tableBody);
  const [page, setPage] = useState(1);

  useEffect(() => {
    if (
      tableBody.length > 0
    ) {
      if (sort) {
        const sortedList = sortBy(tableBody, [sort.key]);
        if (sort.value === "desc") {
          setTableData(sortedList.reverse());
        } else {
          setTableData(sortedList);
        }
      } else {
        setTableData(tableBody);
      }
    } else {
      setTableData([]);
    }
  }, [sort, tableBody]);



  
  const handleSelectedCheckbox = (event) => {
    const checkboxId = event.target.id;
    let data=[...selectedCheckboxIds]
    if (event.target.checked) {
      // setSelectedCheckboxIds([...selectedCheckboxIds, checkboxId]);
      data.push(checkboxId)
    } else {
      const newSelectedUserId = data.filter(
        (id) => id !== checkboxId
      );
    data=newSelectedUserId
    }
    setSelectedCheckboxIds(data)
      onSelectCheckbox&& onSelectCheckbox(data)  
 
 
  };


  const getActionView = (rowData) => {
    return (
      <div className='flex flex-row gap-1'>
        {actionType.includes('Edit') &&
          <div className='' onClick={() => onPressAction && onPressAction(rowData, "Edit")}>
            <Tooltip content="Edit">
              <PencilSquareIcon className="w-6 h-6 text-blue-900" />
            </Tooltip>
          </div>
        }
        {actionType.includes('Delete') &&
          <div className='' onClick={() => onPressAction && onPressAction(rowData, "Delete")}>

            <Tooltip content="Delete">
              <TrashIcon className="w-6 h-6 text-blue-900" />
            </Tooltip>
          </div>
        }
        {actionType.includes('View') &&
          <div className='' onClick={() => onPressAction && onPressAction(rowData, "View")}>

            <Tooltip content="View">
              <EyeIcon className="w-6 h-6 text-blue-900" />
            </Tooltip>
          </div>
        }
        {actionType.includes('Manage') &&
          <div className='' onClick={() => onPressAction && onPressAction(rowData, "Manage")}>

            <Tooltip content="Manage">
              <Cog6ToothIcon className="w-6 h-6 text-blue-900" />
            </Tooltip>
          </div>
        }

        {actionType.includes('Document') &&
          <div className='' onClick={() => onPressAction && onPressAction(rowData, "Document")}>

            <Tooltip content="Document">
              <DocumentIcon className="w-6 h-6 text-blue-900" />
            </Tooltip>
          </div>
        }
        
        { (rowData?.attendees_id && actionType.includes('Link')) &&
          <div className='' onClick={() => onPressAction && onPressAction(rowData, "Link")}>

            <Tooltip content="Link">
              <LinkIcon className="w-6 h-6 text-blue-900" />
            </Tooltip>
          </div>
        }
      </div>
    )
  }

  const onSortClick = (key) => {

    let obj = { key }; //{"username":"username"}
    if (sort && sort.key === key) {
      if (!sort.value) {
        obj["value"] = "asc";
      } else {
        if (sort.value === "asc") {
          obj["value"] = "desc";
        } else if (sort.value === "desc") {
          obj = undefined
        }
      }
    } else {
      obj = { key, value: "asc" };
    }
    setSort(obj);
  };


  const getSortIcon = (key) => {
    if (sort && sort.key === key) {
      if (sort.value === "asc")
        return (
          <BarsArrowUpIcon
            strokeWidth={10}
            className="h-4 w-4"
            color={"#000000"}
          />
        );
      else if (sort.value === "desc")
        return (
          <BarsArrowDownIcon
            strokeWidth={4}
            className="h-4 w-4"
            color={"#000000"}
          />
        );
      else return <Bars3BottomLeftIcon strokeWidth={2} className="h-4 w-4" />;
    } else {
      return <Bars3BottomLeftIcon strokeWidth={2} className="h-4 w-4" />;
    }
  };

  const dateColumn = ["startDate", "endDate", "gradeSubmissionDeadline"]

  const getDateFormat = (date) => {
    if (!date) return "--"
    return moment(date).format("MM/DD/YYYY")

  }
  return (
    <div className="max-w-[100vw] min-w-[50vw] overflow-auto xl:mt-2 2xl:mt-5 ">
      {!loading && tableData.length == 0 ? (
        <div className="w-full h-[62vh] flex flex-row justify-center items-center">
          <NoSymbolIcon
            strokeWidth={4}
            className="h-12 w-12 mr-4 fill-blue-gray-100"
            color={"fill-blue-gray-100"}
          />

          <Typography className="text-2xl text-blue-gray-100 font-semibold">
            No Data Found
          </Typography>
        </div>
      ) :
        <>
          <table className="table-fixed w-full min-h-[300px]">
            <tbody className=" divide-y divide-grey-100 w-full bg-white flex flex-col  overflow-y-scroll items-center justify-between max-h-[62vh] xl:max-h-[48vh]">
              <tr className="flex w-full sticky top-0 z-50 bg-[#1262ab]  ">

                {tableHeader.map((head, index) => (
                  <th key={head.index}
                    onClick={() => onSortClick(head.key)}
                    className={`cursor-pointer ${index < tableHeader.length - 1 ? 'border-r-2' : ''} border-x-blue-gray-200  bg-[#1262ab] p-4 w-full 
                ${index === 0 ? "rounded-tl-none" : ""}
                ${index === tableHeader.length - 1
                        ? "rounded-tr-lg"
                        : " hover:bg-blue-gray-600"
                      }`}
                  >
                    <Typography
                      variant="small"
                      color="blue-gray"
                      className="flex items-center justify-between gap-2 font-normal leading-none text-white truncate "
                    >
                      {head.label}
                      {index !== tableHeader.length - 1 &&
                        getSortIcon(head.key)}
                    </Typography>
                  </th>
                ))}
              </tr>
              {tableData.map((data, index) => {
                const classes = "border-b border-x border-blue-gray-50  flex flex-row w-full items-center h-[60px] ";
                return (<tr className="flex w-full   bg-[#fff]  ">
                  {
                    // Object.keys(data).map((key, indexChild) => tableHeader.findIndex((head) => head.key == key) >= 0 &&
                    tableHeader.map((head, indexChild) =>
                      head.key !== "action" ?
                        <td className={classes}
                          onClick={() => showColumnLink.includes(head.key) ? onClickRow && onClickRow(head.key, data) : {}}>
                          <Typography
                            variant="small"
                            color="blue-gray"
                            className={`${showColumnLink.includes(head.key) ? 'font-normal ml-4 flex  items-center hover:border-blue-900 hover:cursor-pointer hover:border-b' : 'font-normal ml-4 flex  items-center'}`}
                          >
                            {indexChild == 0 &&
                            <>
                              {
                                showCheckbox &&
                                <Checkbox 
                                className="justify-start " 
                                id={data?._id}
                                checked={selectedCheckboxIds.includes(
                                  data._id
                                )}
                                onChange={handleSelectedCheckbox}
                              />
                                                                                          }
                              {showAvatar &&
                                <>
                                  {data?.profilePicture?.url ? (
                                    <Avatar
                                      size="lg"
                                      variant="circular"
                                      className="w-[40px] h-[40px] rounded-full mr-2 ml-1"
                                      src={data.profilePicture?.url}
                                      alt="candice wu"
                                    />
                                  ) : (
                                    <div className="flex w-[40px] h-[40px] rounded-full mr-2 ml-1 bg-blue-700 justify-center items-center text-white font-medium text-2xl" >
                                      {data?.userName
                                        ?.charAt(0)
                                        ?.toUpperCase()}
                                    </div>
                                  )}
                                </>
                              }
                            </>
                            }

                            {
                              (head.key === "isActive" || head.key === "activeStatus") ?
                                data[head.key] === true ?
                                  <div className='text-[#1B5E20] bg-[#4CAF5033] rounded-md px-2 py-1 font-medium'>Active</div> :
                                  <div className='text-white bg-[#f0303033] rounded-md px-2 py-1 font-medium'>
                                    De active</div>

                                :
                                (dateColumn.includes(head.key) ? getDateFormat(data[head.key])
                                  : data[head.key]?
                                  data[head.key]
                                  :
                                  data[head.key]===0?0:  '--')
                            }
                          </Typography>
                        </td>
                        :
                        actionType.length > 0 &&
                        <td className={classes}>
                          <Typography
                            variant="small"
                            color="blue-gray"
                            className="font-normal pl-4"
                          >
                            {getActionView(data)}
                          </Typography>
                        </td>
                    )
                  }
                </tr>)
              })}
            </tbody>
          </table>
          {/* {tableData.length > 0 && (
        <div className="w-full flex justify-end cursor-pointer xl:mt-1">
          <Pagination
            count={course?.displayUserDetails?.count}
            onPageChange={(page) => {
              setPage(page);
              getUsers(page);
            }}
            page={page}
          />
        </div>
      )} */}
          <div className=" xl:mr-4 mt-2 mr-7">
            {tableData.length > 0 && (
              <div className="w-full flex items-end content-end justify-end cursor-pointer xl:mt-1">
                <Pagination
                  count={count}
                  onPageChange={(page) => {
                    setPage(page);
                    onPageChange(page);
                  }}
                  page={page}
                />
              </div>
            )}
          </div>
        </>


      }
    </div>

  )
}
export default GenericTable;
