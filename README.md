 <Accordion
                    open={openExisting === index}
                    className="mb-2 rounded-lg border border-blue-gray-100 text-center shadow-xl "
                  >
                    <AccordionHeader
                      onClick={() => toggleHeader(index, true)}
                      className={`bg-[#264390] text-white ${
                        openExisting == 0
                          ? "rounded-lg rounded-b-none"
                          : "rounded-lg "
                      } h-[40px]  flex justify-between`}
                    >
                      <div className=" w-full flex flex-row justify-between items-center">
                        <div className="flex flex-row items-center">
                          <p className="mt-3 px-4">
                            {element.application.applicationName}
                          </p>
                          {false && (
                            <ExclamationCircleIcon
                              className="w-8 h-8"
                              color={"#f2382e"}
                            />
                          )}
                          {true && (
                            <CheckBadgeIcon
                              className="w-8 h-8"
                              color={"#07e015"}
                            />
                          )}
                        </div>
                        <div className=" flex flex-row">
                          <div className="flex text-white">
                            <PencilSquareIcon className="w-8 h-8 mr-3 bg-[#264390] p-1" />
                            <TrashIcon className="w-8 h-8 bg-[#264390] p-1" />
                          </div>
                          <ChevronDownIcon className="w-8 h-8 ml-2 items-end" />
                        </div>
                      </div>
                    </AccordionHeader>
                    <AccordionBody className="pt-0 text-base font-normal bg-white">
                      <div className="flex flex-row w-full items-center">
                        <Image
                          className="px-3 py-2"
                          src={
                            menuList.filter(
                              (ele: any) => ele.id === element.application.id
                            )[0]?.logo
                          }
                          width={180}
                          height={72}
                          alt="COR Advantage"
                        />
 
                        <div className="grid grid-cols-4 md:grid-cols-1 sm:grid-cols-1 xs:grid-cols-1 gap-4 px-5 py-3 w-full ">
                          <TextInput
                            placeholder="Licence"
                            required={true}
                            crossOrigin={undefined}
                            value={element.license}
                            type="number"
                            label="Licence"
                            onChange={(e: any) => {
                              applications[index].role = e.target.value;
                              setApplications([...applications]);
                            }}
                          />
                          <div className="flex flex-col">
                            <div className="w-full flex ml-3">
                              <div className="text-red-600">*</div>
                              Start Date
                            </div>
 
                            <DatePicker
                              className="h-[44px] border-2 border-[#264390] rounded-md px-2 w-full"
                              selected={new Date(element.startDate)}
                              onChange={(date: any) => {
                                // onValunChange(obj.code, "startDate", date);
                              }}
                              placeholderText="MM/DD/YYYY"
                              // showIcon={true}
                              // icon={
                              //   <CalendarMonthOutlinedIcon className="w-16 h-16 mt-[2px] items-end ml-[90%]" />
                              // }
                              title={"Start Date"}
                              required={true}
                            />
                          </div>
 
                          <div className="flex flex-col">
                            <div className="w-full flex ml-3">
                              <div className="text-red-600">*</div>
                              Subscription Type
                            </div>
                            <HSSelect
                              placeholder="Subscription Type*"
                              options={SUBSCRIPTION_TYPE}
                              getOptionLabel={(option: any) => option.label}
                              getOptionValue={(option: any) => option.value}
                              // value={selectdApp[obj.code].subscription_type}
                              value={SUBSCRIPTION_TYPE}
                              onChange={(obj: any) => {
                                // setRegion(obj);
                                // setRegionError("");
                                // onChangeUserDetails(obj, "organization");
                                // setOrgDetails(obj);
                              }}
                              // error={
                              //   selectdApp[obj.code].subscription_type_error
                              // }
                            />
                          </div>
 
                          <div className="w-[100%] flex flex-col">
                            <div className="w-full flex ml-3">
                              <div className="text-red-600">*</div>
                              Expire Date
                            </div>
 
                            <DatePicker
                              className="h-[44px] border-2 border-[#264390] rounded-md px-2 w-full"
                              selected={new Date(element.expireDate)}
                              onChange={(date: any) => {
                                // onValunChange(obj.code, "endDate", date);
                              }}
                              placeholderText="MM/DD/YYYY"
                              // disabled={!selectdApp[obj.code].startDate}
                              // minDate={selectdApp[obj.code].startDate}
                              // showIcon={true}
                              // icon={
                              //   <CalendarMonthOutlinedIcon className="w-16 h-16 mt-[2px] items-end ml-[90%]" />
                              // }
                              required={true}
                            />
                          </div>
                        </div>
                      </div>
                    </AccordionBody>
                  </Accordion>
