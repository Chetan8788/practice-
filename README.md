
import * as React from "react";
import { useSpring, animated } from "@react-spring/web";
import { Grid, TextField as TextField1 } from "@mui/material";

// import { TextField } from "../../common/TextField/TextField";
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
import { useEffect, useState } from "react";
import { isTextValid } from "../../helpers/validate";
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
  const [joiningStatusValid, setJoiningStatusValid] = useState<boolean>();
  const [joiningTypeValid, setJoiningTypeValid] = useState<boolean>();
  const [joiningStatusRemarkValid, setJoiningStatusRemarkValid] =
    useState<boolean>();
  const [recruiterValid, setRecruiterValid] = useState<boolean>();
  const [teamLeadValid, setTeamLeadValid] = useState<boolean>();
  const [crmValid, setCrmValid] = useState<boolean>();
  const [teamManagerValid, setTeamManagerValid] = useState<boolean>();
  const [seniorManagerValid, setSeniorManagerValid] = useState<boolean>();
  const [assoDirectorValid, setAssoDirectorValid] = useState<boolean>();
  const [centerHeadValid, setCenterHeadValid] = useState<boolean>();
  const [onsiteAccDirectorValid, setOnsiteAccDirectorValid] =
    useState<boolean>();
  const [onboCoordinatorValid, setOnboCoordinatorValid] = useState<boolean>();
  const [endDateValid, setEndDateValid] = useState<boolean>();
  const [exitClearanceValid, setExitClearanceValid] = useState<boolean>();
  const [endReasonValid, setEndReasonValid] = useState<boolean>();
  const [endRemarksValid, setEndRemarksValid] = useState<boolean>();
  const [grossBrValid, setGrossBrValid] = useState<boolean>();
  const [mspFeePercentageValid, setMspFeePercentageValid] = useState<boolean>();
  const [mspFeeValid, setMspFeeValid] = useState<boolean>();
  const [payRateValid, setPayRateValid] = useState<boolean>();
  const [refFeeValid, setRefFeeValid] = useState<boolean>();
  const [taxOHPercentageValid, setTaxOHPercentageValid] = useState<boolean>();
  const [taxOHValid, setTaxOHValid] = useState<boolean>();
  const [hBenefitesOptedValid, setHBenefitesOptedValid] = useState<boolean>();
  const [hBenefitesCostValid, setHBenefitesCostValid] = useState<boolean>();
  const [netBillRateValid, setNetBillRateValid] = useState<boolean>();
  const [netPurchaseValid, setNetPurchaseValid] = useState<boolean>();

  const [marginValid, setMarginValid] = useState<boolean>();
  const [fullTimeSalaryOfferedValid, setFullTimeSalaryOfferedValid] =
    useState<boolean>();
  const [jobLevelValid, setJobLevelValid] = useState<boolean>();
  const [ffInvoiceStatusValid, setFfInvoiceStatusValid] = useState<boolean>();

  const [joiningStatusError, setJoiningStatusError] = useState<any>();
  const [joiningTypeError, setJoiningTypeError] = useState<any>();
  const [joiningStatusRemarkError, setJoiningStatusRemarkError] =
    useState<any>();
  const [recruiterError, setRecruiterError] = useState<any>();
  const [teamLeadError, setTeamLeadError] = useState<any>();
  const [crmError, setCrmError] = useState<any>();
  const [teamManagerError, setTeamManagerError] = useState<any>();
  const [seniorManagerError, setSeniorManagerError] = useState<any>();
  const [assoDirectorError, setAssoDirectorError] = useState<any>();
  const [centerHeadError, setCenterHeadError] = useState<any>();
  const [onsiteAccDirectorError, setOnsiteAccDirectorError] = useState<any>();
  const [onboCoordinatorError, setOnboCoordinatorError] = useState<any>();
  const [endDateError, setEndDateError] = useState<any>();
  const [exitClearanceError, setExitClearanceError] = useState<any>();
  const [endReasonError, setEndReasonError] = useState<any>();
  const [endRemarksError, setEndRemarksError] = useState<any>();
  const [grossBrError, setGrossBrError] = useState<any>();
  const [mspFeePercentageError, setMspFeePercentageError] = useState<any>();
  const [mspFeeError, setMspFeeError] = useState<any>();
  const [payRateError, setPayRateError] = useState<any>();
  const [refFeeError, setRefFeeError] = useState<any>();
  const [taxOHPercentageError, setTaxOHPercentageError] = useState<any>();
  const [taxOHError, setTaxOHError] = useState<any>();
  const [hBenefitesOptedError, setHBenefitesOptedError] = useState<any>();
  const [hBenefitesCostError, setHBenefitesCostError] = useState<any>();
  const [netBillRateError, setNetBillRateError] = useState<any>();
  const [netPurchaseError, setNetPurchaseError] = useState<any>();

  const [marginError, setMarginError] = useState<any>();
  const [fullTimeSalaryOfferedError, setFullTimeSalaryOfferedError] =
    useState<any>();
  const [jobLevelError, setJobLevelError] = useState<any>();
  const [ffInvoiceStatusError, setFfInvoiceStatusError] = useState<any>();

  function updateCandidateStartEndOperations() {
    setJoiningStatusValid(isTextValid(joiningStatus.value));
    setJoiningTypeValid(isTextValid(joiningType.value));
    setJoiningStatusRemarkValid(isTextValid(joiningStatusRemark));
    setRecruiterValid(isTextValid(recruiter));
    setTeamLeadValid(isTextValid(teamLead));
    setCrmValid(isTextValid(crm));
    setTeamManagerValid(isTextValid(teamManager));
    setSeniorManagerValid(isTextValid(seniorManager));
    setAssoDirectorValid(isTextValid(assoDirector));
    setCenterHeadValid(isTextValid(centerHead));
    setOnsiteAccDirectorValid(isTextValid(onsiteAccDirector));
    setOnboCoordinatorValid(isTextValid(onboCoordinator));
    setEndDateValid(isTextValid(endDate));
    setExitClearanceValid(isTextValid(exitClearance.value));
    setEndReasonValid(isTextValid(endReason.value));
    setEndRemarksValid(isTextValid(endRemarks));
    setGrossBrValid(isTextValid(grossBr));
    setMspFeePercentageValid(isTextValid(mspFeePercentage));
    setMspFeeValid(isTextValid(mspFee));
    setPayRateValid(isTextValid(payRate));
    setRefFeeValid(isTextValid(refFee));
    setTaxOHPercentageValid(isTextValid(taxOHPercentage));
    setTaxOHValid(isTextValid(taxOH));
    setHBenefitesOptedValid(isTextValid(hBenefitesOpted.value));
    setHBenefitesCostValid(isTextValid(hBenefitesCost));
    setNetBillRateValid(isTextValid(netBillRate));
    setNetPurchaseValid(isTextValid(netPurchase));
    setMarginValid(isTextValid(margin));
    setFullTimeSalaryOfferedValid(isTextValid(fullTimeSalaryOffered));
    setJobLevelValid(isTextValid(jobLevel.value));
    setFfInvoiceStatusValid(isTextValid(ffInvoiceStatus.value));

    if (
      joiningStatusValid &&
      joiningTypeValid &&
      joiningStatusRemarkValid &&
      recruiterValid &&
      teamLeadValid &&
      crmValid &&
      teamManagerValid &&
      seniorManagerValid &&
      assoDirectorValid &&
      centerHeadValid &&
      onsiteAccDirectorValid &&
      onboCoordinatorValid &&
      endDateValid &&
      exitClearanceValid &&
      endReasonValid &&
      endRemarksValid &&
      grossBrValid &&
      mspFeePercentageValid &&
      mspFeeValid &&
      payRateValid &&
      refFeeValid &&
      taxOHPercentageValid &&
      taxOHValid &&
      hBenefitesOptedValid &&
      hBenefitesCostValid &&
      netBillRateValid &&
      netPurchaseValid &&
      marginValid &&
      fullTimeSalaryOfferedValid &&
      jobLevelValid &&
      ffInvoiceStatusValid
    ) {
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
    } else {
      if (!joiningStatusValid) {
        setJoiningStatusError("Joining status should not be empty.");
      }
      if (!joiningTypeValid) {
        setJoiningTypeError("Joining type should not be empty.");
      }
      if (!joiningStatusRemarkValid) {
        setJoiningStatusRemarkError(
          "Joining satus remark should not be empty."
        );
      }
      if (!recruiterValid) {
        setRecruiterError("Recruiter should not be empty.");
      }
      if (!teamLeadValid) {
        setTeamLeadError("Team lead should not be empty.");
      }
      if (!crmValid) {
        setCrmError("Crm should not be empty.");
      }
      if (!teamManagerValid) {
        setTeamManagerError("Team manager should not be empty.");
      }
      if (!seniorManagerValid) {
        setSeniorManagerError("Senior manager should not be empty.");
      }
      if (!assoDirectorValid) {
        setAssoDirectorError("Assodirector should not be empty.");
      }
      if (!centerHeadValid) {
        setCenterHeadError("Center head should not be empty.");
      }
      if (!onsiteAccDirectorValid) {
        setOnsiteAccDirectorError("Onsite acc director should not be empty.");
      }
      if (!onboCoordinatorValid) {
        setOnboCoordinatorError("Onbo coordinator should not be empty.");
      }
      if (!endDateValid) {
        setEndDateError("End date should not be empty.");
      }
      if (!exitClearanceValid) {
        setExitClearanceError("Exit clearance should not be empty.");
      }
      if (!endReasonValid) {
        setEndReasonError("End reason should not be empty.");
      }
      if (!endRemarksValid) {
        setEndRemarksError("End remarks should not be empty.");
      }
      if (!grossBrValid) {
        setGrossBrError("Grossbr should not be empty.");
      }
      if (!mspFeePercentageValid) {
        setMspFeePercentageError("Msp fee percentage should not be empty.");
      }
      if (!mspFeeValid) {
        setMspFeeError("Msp fee should not be empty.");
      }
      if (!payRateValid) {
        setPayRateError("Pay rate should not be empty.");
      }
      if (!refFeeValid) {
        setRefFeeError("Ref fee should not be empty.");
      }
      if (!taxOHPercentageValid) {
        setTaxOHPercentageError("Tax oh percentage should not be empty.");
      }
      if (!taxOHValid) {
        setTaxOHError("Tax oh should not be empty.");
      }
      if (!hBenefitesOptedValid) {
        setHBenefitesOptedError("Hbenefites opted should not be empty.");
      }
      if (!hBenefitesCostValid) {
        setHBenefitesCostError("Hbenefites cost should not be empty.");
      }
      if (!netBillRateValid) {
        setNetBillRateError("Net bill rate should not be empty.");
      }
      if (!netPurchaseValid) {
        setNetPurchaseError("Net purchase should not be empty.");
      }
      if (!marginValid) {
        setMarginError("Margin should not be empty.");
      }
      if (!fullTimeSalaryOfferedValid) {
        setFullTimeSalaryOfferedError(
          "Full time salary Offered should not be empty."
        );
      }
      if (!jobLevelValid) {
        setJobLevelError("Job level should not be empty.");
      }
      if (!ffInvoiceStatusValid) {
        setFfInvoiceStatusError("FfInvoice status should not be empty.");
      }
    }
  }
  return (
    <div className="pt-10 pl-10 h-[60vh] overflow-auto" id="no-scroll-div">
      <Grid container spacing={2} columnGap={"15px"}>
        <Grid xs={6} md={5.5}>
          <Select
            aria-label="state"
            className="text-[13px] text-left"
            options={JoiningStatusList}
            placeholder="state"
            value={joiningStatus}
            getOptionLabel={(option) => option.label}
            getOptionValue={(option) => option.value}
            onChange={(e: any) => {
              setJoiningStatus(e);
              setJoiningStatusValid(isTextValid(e?.value));
              if (!joiningStatusValid) {
                setJoiningStatusError("State should not be empty.");
              }
            }}
            isSearchable={true}
          />
          {!joiningStatusValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {joiningStatusError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <Select
            aria-label="joining Type"
            className="text-[13px] text-left"
            options={JoiningTypeList}
            placeholder="state"
            value={joiningType}
            getOptionLabel={(option) => option.label}
            getOptionValue={(option) => option.value}
            onChange={(e: any) => {
              setJoiningType(e);
              setJoiningTypeValid(isTextValid(e?.value));
              if (!joiningTypeValid) {
                setJoiningTypeError("Joining type should not be empty.");
              }
            }}
            isSearchable={true}
          />
          {!joiningTypeValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "15px" }}
            >
              {joiningTypeError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Joining status remark"
            value={joiningStatusRemark}
            placeholder={""}
            handleChange={(event) => {
              setJoiningStatusRemark(event.target.value);
              setJoiningStatusRemarkValid(isTextValid(event.target.value));
              if (!joiningStatusRemarkValid) {
                setJoiningStatusRemarkError(
                  "Joining status remark should not be empty."
                );
              }
            }}
            className=""
          />
          {!joiningStatusRemarkValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {joiningStatusRemarkError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Recruiter"
            value={recruiter}
            placeholder={""}
            handleChange={(event) => {
              setRecruiter(event.target.value);
              setRecruiterValid(isTextValid(event.target.value));
              if (!recruiterValid) {
                setRecruiterError("Recruiter should not be empty.");
              }
            }}
            className=""
          />
          {!recruiterValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {recruiterError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Team lead"
            value={teamLead}
            placeholder={""}
            handleChange={(event) => {
              setTeamLead(event.target.value);
              setTeamLeadValid(isTextValid(event.target.value));
              if (!teamLeadValid) {
                setTeamLeadError("Team lead should not be empty.");
              }
            }}
            className=""
          />
          {!teamLeadValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {teamLeadError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="crm"
            value={crm}
            placeholder={""}
            handleChange={(event) => {
              setCrm(event.target.value);
              setCrmValid(isTextValid(event.target.value));
              if (!crmValid) {
                setCrmError("Crm should not be empty.");
              }
            }}
            className=""
          />
          {!crmValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {crmError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Team manager"
            value={teamManager}
            placeholder={""}
            handleChange={(event) => {
              setTeamManager(event.target.value);
              setTeamManagerValid(isTextValid(event.target.value));
              if (!teamManagerValid) {
                setTeamManagerError("Team manager should not be empty.");
              }
            }}
            className=""
          />
          {!teamManagerValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {teamManagerError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Senior manager"
            value={seniorManager}
            placeholder={""}
            handleChange={(event) => {
              setSeniorManager(event.target.value);
              setSeniorManagerValid(isTextValid(event.target.value));
              if (!seniorManagerValid) {
                setSeniorManagerError("Senior manager should not be empty.");
              }
            }}
            className=""
          />
          {!seniorManagerValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {seniorManagerError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Associate director"
            value={assoDirector}
            placeholder={""}
            handleChange={(event) => {
              setAssoDirector(event.target.value);
              setAssoDirectorValid(isTextValid(event.target.value));
              if (!assoDirectorValid) {
                setAssoDirectorError("Associate director should not be empty.");
              }
            }}
            className=""
          />
          {!assoDirectorValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {assoDirectorError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Center head"
            value={centerHead}
            placeholder={""}
            handleChange={(event) => {
              setCenterHead(event.target.value);
              setCenterHeadValid(isTextValid(event.target.value));
              if (!centerHeadValid) {
                setCenterHeadError("Center head should not be empty.");
              }
            }}
            className=""
          />
          {!centerHeadValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {centerHeadError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Onsite account director"
            value={onsiteAccDirector}
            placeholder={""}
            handleChange={(event) => {
              setOnsiteAccDirector(event.target.value);
              setOnsiteAccDirectorValid(isTextValid(event.target.value));
              if (!onsiteAccDirectorValid) {
                setOnsiteAccDirectorError(
                  "Onsite account director should not be empty."
                );
              }
            }}
            className=""
          />
          {!onsiteAccDirectorValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {onsiteAccDirectorError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Onboarding coordinator"
            value={onboCoordinator}
            placeholder={""}
            handleChange={(event) => {
              setOnboCoordinator(event.target.value);
              setOnboCoordinatorValid(isTextValid(event.target.value));
              if (!onboCoordinatorValid) {
                setOnboCoordinatorError(
                  "Onboarding coordinator should not be empty."
                );
              }
            }}
            className=""
          />
          {!onboCoordinatorValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {onboCoordinatorError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="End date"
            type="date"
            value={endDate}
            placeholder={""}
            handleChange={(event) => {
              setEndDate(event.target.value);
              setEndDateValid(isTextValid(event.target.value));
              if (!endDateValid) {
                setEndDateError("End date should not be empty.");
              }
            }}
            className=""
          />
          {!endDateValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {endDateError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <Select
            aria-label="Exit clearance"
            className="text-[13px] text-left"
            options={ExitClearanceList}
            placeholder="Exit clearance"
            value={exitClearance}
            getOptionLabel={(option) => option.label}
            getOptionValue={(option) => option.value}
            onChange={(e: any) => {
              setExitClearance(e);
              setExitClearanceValid(isTextValid(e?.value));
              if (!exitClearanceValid) {
                setExitClearanceError("Exit clearance should not be empty.");
              }
            }}
            isSearchable={true}
          />
          {!exitClearanceValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {exitClearanceError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <Select
            aria-label="End reason"
            className="text-[13px] text-left"
            options={EndReasonList}
            placeholder="End reason"
            value={endReason}
            getOptionLabel={(option) => option.label}
            getOptionValue={(option) => option.value}
            onChange={(e: any) => {
              setEndReason(e);
              setEndReasonValid(isTextValid(e?.value));
              if (!endReasonValid) {
                setEndReasonError("End reason should not be empty.");
              }
            }}
            isSearchable={true}
          />
          {!endReasonValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {endReasonError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="End remarks"
            value={endRemarks}
            placeholder={""}
            handleChange={(event) => {
              setEndRemarks(event.target.value);
              setEndRemarksValid(isTextValid(event.target.value));
              if (!endRemarksValid) {
                setEndRemarksError("End remarks should not be empty.");
              }
            }}
            className=""
          />
          {!endRemarksValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {endRemarksError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Gross BR"
            value={grossBr}
            placeholder={""}
            handleChange={(event) => {
              setGrossBr(event.target.value);
              setGrossBrValid(isTextValid(event.target.value));
              if (!grossBrValid) {
                setGrossBrError("Gross BR should not be empty.");
              }
            }}
            className=""
          />
          {!grossBrValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {grossBrError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="MSP fee percentage"
            value={mspFeePercentage}
            placeholder={""}
            handleChange={(event) => {
              setMspFeePercentage(event.target.value);
              setMspFeePercentageValid(isTextValid(event.target.value));
              if (!mspFeePercentageValid) {
                setMspFeePercentageError(
                  "MSP fee percentage should not be empty."
                );
              }
            }}
            className=""
          />
          {!mspFeePercentageValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {mspFeePercentageError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="MSP fee"
            value={mspFee}
            placeholder={""}
            handleChange={(event) => {
              setMspFee(event.target.value);
              setMspFeeValid(isTextValid(event.target.value));
              if (!mspFeeValid) {
                setMspFeeError("MSP fee should not be empty.");
              }
            }}
            className=""
          />
          {!mspFeeValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {mspFeeError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Pay rate"
            value={payRate}
            placeholder={""}
            handleChange={(event) => {
              setPayRate(event.target.value);
              setPayRateValid(isTextValid(event.target.value));
              if (!payRateValid) {
                setPayRateError("Pay rate should not be empty.");
              }
            }}
            className=""
          />
          {!payRateValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {payRateError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Ref Fee"
            value={refFee}
            placeholder={""}
            handleChange={(event) => {
              setRefFee(event.target.value);
              setRefFeeValid(isTextValid(event.target.value));
              if (!refFeeValid) {
                setRefFeeError("Ref Fee should not be empty.");
              }
            }}
            className=""
          />
          {!refFeeValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {refFeeError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Tax OH percentage"
            value={taxOHPercentage}
            placeholder={""}
            handleChange={(event) => {
              setTaxOHPercentage(event.target.value);
              setTaxOHPercentageValid(isTextValid(event.target.value));
              if (!taxOHPercentageValid) {
                setRefFeeError("Tax OH percentage should not be empty.");
              }
            }}
            className=""
          />
          {!refFeeValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {refFeeError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Tax OH"
            value={taxOH}
            placeholder={""}
            handleChange={(event) => {
              setTaxOH(event.target.value);
              setTaxOHValid(isTextValid(event.target.value));
              if (!taxOHValid) {
                setTaxOHError("Tax OH should not be empty.");
              }
            }}
            className=""
          />
          {!taxOHValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {taxOHError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <Select
            aria-label="Health benefits opted"
            className="text-[13px] text-left"
            options={yesNoList}
            placeholder="Health benefits opted"
            value={hBenefitesOpted}
            getOptionLabel={(option) => option.label}
            getOptionValue={(option) => option.value}
            onChange={(e: any) => {
              setHBenefitesOpted(e);
              setHBenefitesOptedValid(isTextValid(e?.value));
              if (!hBenefitesOptedValid) {
                setHBenefitesOptedError(
                  "Health benefits opted should not be empty."
                );
              }
            }}
            isSearchable={true}
          />
          {!hBenefitesOptedValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {hBenefitesOptedError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Health benefits cost"
            value={hBenefitesCost}
            placeholder={""}
            handleChange={(event) => {
              setHBenefitesCost(event.target.value);
              setHBenefitesCostValid(isTextValid(event.target.value));
              if (!hBenefitesCostValid) {
                setHBenefitesCostError(
                  "Health benefits cost should not be empty."
                );
              }
            }}
            className=""
          />
          {!hBenefitesCostValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {hBenefitesCostError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="netBillRate"
            value={netBillRate}
            placeholder={""}
            handleChange={(event) => {
              setNetBillRate(event.target.value);
              setNetBillRateValid(isTextValid(event.target.value));
              if (!netBillRateValid) {
                setNetBillRateError("netBillRate should not be empty.");
              }
            }}
            className=""
          />
          {!netBillRateValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {netBillRateError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Net purchase"
            value={netPurchase}
            placeholder={""}
            handleChange={(event) => {
              setNetPurchase(event.target.value);
              setNetPurchaseValid(isTextValid(event.target.value));
              if (!netPurchaseValid) {
                setNetPurchaseError("Net purchase should not be empty.");
              }
            }}
            className=""
          />
          {!netPurchaseValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {netPurchaseError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Margin"
            value={margin}
            placeholder={""}
            handleChange={(event) => {
              setMargin(event.target.value);
              setMarginValid(isTextValid(event.target.value));
              if (!marginValid) {
                setMarginError("Margin should not be empty.");
              }
            }}
            className=""
          />
          {!marginValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {marginError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <FloatLabel
            label="Full time salary offered"
            value={fullTimeSalaryOffered}
            placeholder={""}
            handleChange={(event) => {
              setFullTimeSalaryOffered(event.target.value);
              setFullTimeSalaryOfferedValid(isTextValid(event.target.value));
              if (!fullTimeSalaryOfferedValid) {
                setFullTimeSalaryOfferedError(
                  "Full time salary offered should not be empty."
                );
              }
            }}
            className=""
          />
          {!fullTimeSalaryOfferedValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {fullTimeSalaryOfferedError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <Select
            aria-label="jobLevel"
            className="text-[13px] text-left"
            options={JobLevelList}
            placeholder="jobLevel"
            value={jobLevel}
            getOptionLabel={(option) => option.label}
            getOptionValue={(option) => option.value}
            onChange={(e: any) => {
              setJobLevel(e);
              setJobLevelValid(isTextValid(e?.value));
              if (!jobLevelValid) {
                setJobLevelError("jobLevel should not be empty.");
              }
            }}
            isSearchable={true}
          />
          {!jobLevelValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {jobLevelError}
            </p>
          ) : null}
        </Grid>

        <Grid xs={6} md={5.5}>
          <Select
            aria-label="FF invoice status"
            className="text-[13px] text-left"
            options={FFInvoiceStatusList}
            placeholder="FF invoice status"
            value={ffInvoiceStatus}
            getOptionLabel={(option) => option.label}
            getOptionValue={(option) => option.value}
            onChange={(e: any) => {
              setFfInvoiceStatus(e);
              setFfInvoiceStatusValid(isTextValid(e?.value));
              if (!ffInvoiceStatusValid) {
                setFfInvoiceStatusError(
                  "FF invoice status should not be empty."
                );
              }
            }}
            isSearchable={true}
          />
          {!ffInvoiceStatusValid ? (
            <p
              className=""
              style={{ fontSize: "12px", color: "red", marginBottom: "5px" }}
            >
              {ffInvoiceStatusError}
            </p>
          ) : null}
        </Grid>
      </Grid>
      <div className="m-auto w-[30%] ml-[30%] text-white">
        <Button
          className=""
          value="update"
          handleClick={() => {
            updateCandidateStartEndOperations();
          }}
        />
      </div>
    </div>
  );
};

export default ShowStartEndOperations;
