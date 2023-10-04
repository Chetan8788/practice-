// import * as React from 'react';
import React, { useState } from "react";
import { useSpring, animated } from "@react-spring/web";
import { TextField } from "../../common/TextField/TextField";
import { useAppDispatch, useAppSelector } from "../../hooks/app";
import {
  EndReasonList,
  ExitClearanceList,
  FFInvoiceStatusList,
  JobLevelList,
  JoiningStatusList,
  JoiningTypeList,
  yesNoList,
} from "../../constants/constants";
import Select from "react-select";
import moment from "moment";
import { Button } from "../../common/Button/Button";
import { editCandidateStartEndOperationsData } from "../../actions/startendoperations";
import { RootState } from "../../redux/store";
import { Grid } from "@mui/material";
import { FloatLabel } from "../../common/FloatLabel/FloatLabel";

interface FadeProps {
  children: React.ReactElement;
  in?: boolean;
  onClick?: any;
  onEnter?: (node: HTMLElement, isAppearing: boolean) => void;
  onExited?: (node: HTMLElement, isAppearing: boolean) => void;
  ownerState?: any;
}

const Fade = React.forwardRef<HTMLDivElement, FadeProps>(function Fade(
  props,
  ref
) {
  const {
    children,
    in: open,
    onClick,
    onEnter,
    onExited,
    ownerState,
    ...other
  } = props;
  const style = useSpring({
    from: { opacity: 0 },
    to: { opacity: open ? 1 : 0 },
    onStart: () => {
      if (open && onEnter) {
        onEnter(null as any, true);
      }
    },
    onRest: () => {
      if (!open && onExited) {
        onExited(null as any, true);
      }
    },
  });

  return (
    <animated.div ref={ref} style={style} {...other}>
      {React.cloneElement(children, { onClick })}
    </animated.div>
  );
});

const style = {
  position: "absolute" as "absolute",
  top: "50%",
  left: "50%",
  transform: "translate(-50%, -50%)",
  width: 400,
  bgcolor: "background.paper",
  border: "1px #000",
  boxShadow: 24,
  p: 4,
  borderRadius: "10px",
};

interface Props {
  open: any;
  setOpen: any;
  data: any;
  showTableCount: any;
  int: any;
  setShowModal: any;
}

const ShowStartEndOperations: React.FC<Props> = ({
  open,
  setOpen,
  // data,
  showTableCount,
  int,
  setShowModal,
}) => {
  const dispatch = useAppDispatch();
  let data = useAppSelector(
    (state: RootState) => state?.startEndOperations?.singleStartEndOperationData
  );
  const [disable, setDisable] = React.useState(true);

  const [joiningStatus, setJoiningStatus] = React.useState({
    value: data?.joiningStatus,
    label: data?.joiningStatus,
  });

  const [joiningType, setJoiningType] = React.useState({
    value: data?.joiningType,
    label: data?.joiningType,
  });

  const [joiningStatusRemark, setJoiningStatusRemark] = React.useState(
    data?.joiningStatusRemark
  );
  const [recruiter, setRecruiter] = React.useState(data?.recruiter);
  const [teamLead, setTeamLead] = React.useState(data?.teamLead);
  const [crm, setCrm] = React.useState(data?.crm);
  const [teamManager, setTeamManager] = React.useState(data?.teamManager);
  const [seniorManager, setSeniorManager] = React.useState(data?.seniorManager);
  const [assoDirector, setAssoDirector] = React.useState(data?.assoDirector);
  const [centerHead, setCenterHead] = React.useState(data?.centerHead);
  const [onsiteAccDirector, setOnsiteAccDirector] = React.useState(
    data?.onsiteAccDirector
  );
  const [onboCoordinator, setOnboCoordinator] = React.useState(
    data?.onboCoordinator
  );
  const [endDate, setEndDate] = React.useState(
    moment.utc(data?.endDate).format("YYYY-MM-DD")
  );
  const [exitClearance, setExitClearance] = React.useState({
    value: data?.exitClearance,
    label: data?.exitClearance,
  });

  const [JoiningstatusValid, setJoiningstatusValid] = useState<boolean>();
  const [JoiningtypeValid, setJoiningtypeValid] = useState<boolean>();
  const [JoiningstatusremarkValid, setJoiningstatusremarkValid] =
    useState<boolean>();
  const [RecruiterValid, setRecruiterValid] = useState<boolean>();
  const [TeamleadValid, setTeamleadValid] = useState<boolean>();
  const [crmValid, setcrmValid] = useState<boolean>();
  const [teamManagerValid, setteamManagerValid] = useState<boolean>();
  const [seniorManagerValid, setseniorManagerValid] = useState<boolean>();
  const [assoDirectorValid, setassoDirectoryValid] = useState<boolean>();
  const [centerHeadValid, setcenterHeadValid] = useState<boolean>();
  const [onsiteAccDirectorValid, setonsiteAccDirectorValid] =
    useState<boolean>();
  const [onboCoordinatorValid, setonboCoordinatorValid] = useState<boolean>();
  const [EnddateValid, setEnddateValid] = useState<boolean>();
  const [ExitclearanceValid, setExitclearanceValid] = useState<boolean>();
  const [EndremarksValid, setEndremarksValid] = useState<boolean>();
  const [EndreasonValid, setEndreasonValid] = useState<boolean>();
  const [GrossBRValid, setGrossBRValid] = useState<boolean>();
  const [MSPfeepercentageValid, setMSPfeepercentageValid] = useState<boolean>();
  const [MSPfeeValid, setMSPfeeValid] = useState<boolean>();
  const [PayrateValid, setPayrateValid] = useState<boolean>();
  const [RefFeeValid, setRefFeeValid] = useState<boolean>();
  const [TaxOHpercentageValid, setTaxOHpercentageValid] = useState<boolean>();
  const [TaxOHValid, setTaxOHValid] = useState<boolean>();
  const [HealthbenefitsoptedValid, setHealthbenefitsoptedValid] =
    useState<boolean>();
  const [HealthbenefitscostValid, setHealthbenefitscostValid] =
    useState<boolean>();
  const [netBillRateValid, setnetBillRateValid] = useState<boolean>();
  const [netPurchaseValid, setnetPurchaseValid] = useState<boolean>();
  const [marginValid, setmarginValid] = useState<boolean>();
  const [fullTimeSalaryOfferedValid, setfullTimeSalaryOfferedValid] =
    useState<boolean>();
  const [jobLevelValid, setjobLevelValid] = useState<boolean>();
  const [ffInvoiceStatusValid, setffInvoiceStatusValid] = useState<boolean>();
  const [JoiningstatusError, setJoiningstatusError] = useState<any>();
  const [JoiningtypeError, setJoiningtypeError] = useState<any>();
  const [JoiningstatusremarkError, setJoiningstatusremarkError] =
    useState<any>();
  const [RecruiterError, setRecruiterError] = useState<any>();
  const [TeamleadError, setTeamleadError] = useState<any>();
  const [crmError, setCrmError] = useState<any>();
  const [teamManagerError, setStateError] = useState<any>();
  const [seniorManagerError, setseniorManagerError] = useState<any>();
  const [assoDirectorError, setassoDirectorError] = useState<any>();
  const [centerHeadError, setcenterHeadError] = useState<any>();
  const [onboCoordinatorError, setonboCoordinatorError] = useState<any>();
  const [onsiteAccDirectorError, setonsiteAccDirectorError] = useState<any>();
  const [EnddateError, setEnddateError] = useState<any>();
  const [ExitclearanceError, setExitclearanceError] = useState<any>();
  const [EndremarksError, setEndremarksError] = useState<any>();
  const [EndreasonError, setEndreasonError] = useState<any>();
  const [GrossBRError, setGrossBRError] = useState<any>();
  const [MSPfeepercentageError, setMSPfeepercentageError] = useState<any>();
  const [MSPfeeError, setMSPfeeError] = useState<any>();
  const [PayrateError, setPayrateError] = useState<any>();
  const [RefFeeError, setRefFeeError] = useState<any>();
  const [TaxOHpercentageError, setTaxOHpercentageError] = useState<any>();
  const [TaxOHError, setTaxOHError] = useState<any>();
  const [HealthbenefitsoptedError, setHealthbenefitsoptedError] =
    useState<any>();
  const [netBillRateError, setnetBillRateError] = useState<any>();
  const [HealthbenefitscostError, setHealthbenefitscostError] = useState<any>();
  const [netPurchaseError, setnetPurchaseError] = useState<any>();
  const [marginError, setmarginError] = useState<any>();
  const [fullTimeSalaryOfferedError, setfullTimeSalaryOfferedError] =
    useState<any>();
  const [jobLevelError, setjobLevelError] = useState<any>();
  const [ffInvoiceStatusError, setffInvoiceStatusError] = useState<boolean>();
  const [endReason, setEndReason] = React.useState({
    value: data?.endReason,
    label: data?.endReason,
  });

  const [endRemarks, setEndRemarks] = React.useState(data?.endRemarks);
  const [grossBr, setGrossBr] = React.useState(data?.grossBr);
  const [mspFeePercentage, setMspFeePercentage] = React.useState(
    data?.mspFeePercentage
  );
  const [mspFee, setMspFee] = React.useState(data?.mspFee);
  const [payRate, setPayRate] = React.useState(data?.payRate);
  const [refFee, setRefFee] = React.useState(data?.refFee);
  const [taxOHPercentage, setTaxOHPercentage] = React.useState(
    data?.taxOHPercentage
  );
  const [taxOH, setTaxOH] = React.useState(data?.taxOH);

  const [hBenefitesOpted, setHBenefitesOpted] = React.useState({
    value: data?.hBenefitesOpted,
    label: data?.hBenefitesOpted,
  });

  const [hBenefitesCost, setHBenefitesCost] = React.useState(
    data?.hBenefitesCost
  );
  const [netBillRate, setNetBillRate] = React.useState(data?.netBillRate);
  const [netPurchase, setNetPurchase] = React.useState(data?.netPurchase);
  const [margin, setMargin] = React.useState(data?.margin);
  const [fullTimeSalaryOffered, setFullTimeSalaryOffered] = React.useState(
    data?.fullTimeSalaryOffered
  );

  const [jobLevel, setJobLevel] = React.useState({
    value: data?.jobLevel,
    label: data?.jobLevel,
  });
  const [ffInvoiceStatus, setFfInvoiceStatus] = React.useState({
    value: data?.ffInvoiceStatus,
    label: data?.ffInvoiceStatus,
  });
  const [count, setCount] = React.useState(0);

  React.useEffect(() => {
    setJoiningStatus({
      value: data?.joiningStatus,
      label: data?.joiningStatus,
    });
    setJoiningType({
      value: data?.joiningType,
      label: data?.joiningType,
    });

    setJoiningStatusRemark(data?.joiningStatusRemark);
    setRecruiter(data?.recruiter);
    setTeamLead(data?.teamLead);
    setCrm(data?.crm);
    setTeamManager(data?.teamManager);
    setSeniorManager(data?.seniorManager);
    setAssoDirector(data?.assoDirector);
    setCenterHead(data?.centerHead);
    setOnsiteAccDirector(data?.onsiteAccDirector);
    setOnboCoordinator(data?.onboCoordinator);
    setEndDate(moment.utc(data?.endDate).format("YYYY-MM-DD"));

    setExitClearance({
      value: data?.exitClearance,
      label: data?.exitClearance,
    });

    setEndReason({
      value: data?.endReason,
      label: data?.endReason,
    });

    setEndRemarks(data?.endRemarks);
    setGrossBr(data?.grossBr);
    setMspFeePercentage(data?.mspFeePercentage);
    setMspFee(data?.mspFee);
    setPayRate(data?.payRate);
    setRefFee(data?.refFee);
    setTaxOHPercentage(data?.taxOHPercentage);
    setTaxOH(data?.taxOH);

    setHBenefitesOpted({
      value: data?.hBenefitesOpted,
      label: data?.hBenefitesOpted,
    });

    setHBenefitesCost(data?.hBenefitesCost);
    setNetBillRate(data?.netBillRate);
    setNetPurchase(data?.netPurchase);
    setMargin(data?.margin);
    setFullTimeSalaryOffered(data?.fullTimeSalaryOffered);

    setJobLevel({
      value: data?.jobLevel,
      label: data?.jobLevel,
    });
    setFfInvoiceStatus({
      value: data?.ffInvoiceStatus,
      label: data?.ffInvoiceStatus,
    });
    setCount(1);
    // }
  }, [data]);

  function updateCandidateStartEndOperations() {
    // console.log('voidCheckOrEmailContent: ', voidCheckOrEmailContent);
    dispatch(
      editCandidateStartEndOperationsData(
        joiningStatus,
        joiningType,
        joiningStatusRemark,
        recruiter,
        teamLead,
        crm,
        teamManager,
        seniorManager,
        assoDirector,
        centerHead,
        onsiteAccDirector,
        onboCoordinator,
        endDate,
        exitClearance,
        endReason,
        endRemarks,
        grossBr,
        mspFeePercentage,
        mspFee,
        payRate,
        refFee,
        taxOHPercentage,
        taxOH,
        hBenefitesOpted,
        hBenefitesCost,
        netBillRate,
        netPurchase,
        margin,
        fullTimeSalaryOffered,
        jobLevel,
        ffInvoiceStatus,
        data?.candidateId
      )
    );
    setShowModal(false);
  }

  return (
    <>
      <div className="pt-5 mx-auto px-5">
        <Grid container gap={1}>
          <Grid xs={6} md={5.9}>
            <Select
              placeholder="Joining status"
              options={JoiningStatusList}
              value={joiningStatus}
              onChange={(e: any) => setJoiningStatus(e)}
              isSearchable={true}
            />
            {!JoiningstatusValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {JoiningstatusError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <Select
              placeholder="Joining type"
              options={JoiningTypeList}
              value={joiningType}
              onChange={(e: any) => setJoiningType(e)}
              isSearchable={true}
            />
            {!JoiningtypeValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {JoiningtypeError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              className=""
              label="*Joining status remark"
              value={joiningStatusRemark}
              placeholder={""}
              handleChange={(e: any) => {
                setJoiningStatusRemark(e.target.value);
              }}
            />
            {!JoiningstatusremarkValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {JoiningstatusremarkError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Recruiter"
              value={recruiter}
              placeholder={""}
              handleChange={(e: any) => {
                setRecruiter(e.target.value);
              }}
              className="p-5"
            />
            {!RecruiterValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {RecruiterError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Team lead"
              value={teamLead}
              placeholder={""}
              handleChange={(e: any) => {
                setRecruiter(e.target.value);
              }}
              className=""
            />
            {!TeamleadValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {TeamleadError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*crm"
              value={crm}
              placeholder={""}
              handleChange={(e: any) => {
                setCrm(e.target.value);
              }}
              className=""
            />
            {!crmValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {crmError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Team manager"
              value={teamManager}
              placeholder={""}
              handleChange={(e: any) => {
                setTeamManager(e.target.value);
              }}
              className=""
            />
            {!teamManagerValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {teamManagerError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Senior manager"
              value={seniorManager}
              placeholder={""}
              handleChange={(e: any) => {
                setSeniorManager(e.target.value);
              }}
              className=""
            />
            {!seniorManagerValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {seniorManagerError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Associate director"
              value={assoDirector}
              placeholder={""}
              handleChange={(e: any) => {
                setAssoDirector(e.target.value);
              }}
              className=""
            />
            {!assoDirectorValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {assoDirectorError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Center head"
              value={centerHead}
              handleChange={(e: any) => {
                setCenterHead(e.target.value);
              }}
              className=""
            />
            {!centerHeadValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {centerHeadError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Onsite account director"
              value={onboCoordinator}
              handleChange={(e: any) => {
                setOnboCoordinator(e.target.value);
              }}
              className=""
            />
            {!onboCoordinatorValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {onboCoordinatorError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Onboarding coordinator"
              value={onsiteAccDirector}
              handleChange={(e: any) => {
                setOnboCoordinator(e.target.value);
              }}
              className=""
            />
            {!onsiteAccDirectorValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {onsiteAccDirectorError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*End date"
              value={endDate}
              type="date"
              handleChange={(e: any) => {
                setEndDate(e.target.value);
              }}
            />
            {!EnddateValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {EnddateError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <Select
              placeholder="Exit clearance"
              value={exitClearance}
              options={ExitClearanceList}
              onChange={(e: any) => setExitClearance(e)}
            />
            {!ExitclearanceValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {ExitclearanceError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <Select
              placeholder="End reason"
              value={endReason}
              options={EndReasonList}
              onChange={(e: any) => setEndReason(e)}
            />

            {!EndreasonValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {EndreasonError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*End remarks"
              value={endRemarks}
              handleChange={(e: any) => {
                setEndRemarks(e.target.value);
              }}
            />
            {!EndremarksValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {EndremarksError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Gross BR"
              value={grossBr}
              handleChange={(e: any) => {
                setGrossBr(e.target.value);
              }}
            />
            {!GrossBRValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {GrossBRError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*MSP fee percentage"
              value={mspFeePercentage}
              handleChange={(e: any) => {
                setMspFeePercentage(e.target.value);
              }}
            />
            {!MSPfeepercentageValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {MSPfeepercentageError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*MSP fee percentage"
              value={mspFee}
              handleChange={(e: any) => {
                setMspFee(e.target.value);
              }}
            />
            {!MSPfeeValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {MSPfeeError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Pay rate"
              value={payRate}
              handleChange={(e: any) => {
                setPayRate(e.target.value);
              }}
            />
            {!PayrateValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {PayrateError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Ref Fee"
              value={refFee}
              handleChange={(e: any) => {
                setRefFee(e.target.value);
              }}
            />
            {!RefFeeValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {RefFeeError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Tax OH percentage"
              value={taxOHPercentage}
              handleChange={(e: any) => {
                setTaxOHPercentage(e.target.value);
              }}
            />
            {!TaxOHpercentageValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {TaxOHpercentageError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Tax OH "
              value={taxOH}
              handleChange={(e: any) => {
                setTaxOH(e.target.value);
              }}
            />
            {!TaxOHValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {TaxOHError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <Select
              placeholder="Health benefits opted"
              value={hBenefitesOpted}
              options={yesNoList}
              onChange={(e: any) => setHBenefitesOpted(e)}
            />
            {!HealthbenefitsoptedValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {HealthbenefitsoptedError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Healthbenefitscost"
              value={hBenefitesCost}
              handleChange={(e: any) => {
                setHBenefitesCost(e.target.value);
              }}
            />
            {!HealthbenefitscostValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {HealthbenefitscostError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*netBillRate"
              value={netBillRate}
              handleChange={(e: any) => {
                setNetBillRate(e.target.value);
              }}
            />
            {!netBillRateValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {netBillRateError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Net purchase"
              value={netPurchase}
              handleChange={(e: any) => {
                setNetPurchase(e.target.value);
              }}
            />
            {!netPurchaseValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {netPurchaseError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Margin"
              value={margin}
              handleChange={(e: any) => {
                setMargin(e.target.value);
              }}
            />
            {!marginValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {marginError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <FloatLabel
              label="*Full time salary offered"
              value={fullTimeSalaryOffered}
              handleChange={(e: any) => {
                setFullTimeSalaryOffered(e.target.value);
              }}
            />
            {!fullTimeSalaryOfferedValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {fullTimeSalaryOfferedError}
              </p>
            ) : null}
          </Grid>
          <Grid xs={6} md={5.9}>
            <Select
              placeholder="jobLevel"
              value={jobLevel}
              options={JobLevelList}
              onChange={(e: any) => setJobLevel(e)}
            />
            {!jobLevelValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {jobLevelError}
              </p>
            ) : null}
          </Grid>

          <Grid xs={6} md={5.9}>
            <Select
              placeholder="FF invoice status"
              value={ffInvoiceStatus}
              options={FFInvoiceStatusList}
              onChange={(e: any) => setFfInvoiceStatus(e)}
            />
            {!ffInvoiceStatusValid ? (
              <p className="" style={{ fontSize: "12px", color: "red" }}>
                {ffInvoiceStatusError}
              </p>
            ) : null}
          </Grid>
        </Grid>
        {/* <Grid xs={12} md={12}> */}
        <div className="m-auto w-[50%]">
          <Button
            className="w-[50px] text-white"
            value="update"
            handleClick={() => {
              updateCandidateStartEndOperations();
            }}
          />
        </div>
        {/* </Grid> */}
      </div>
    </>
  );
};

export default ShowStartEndOperations;
