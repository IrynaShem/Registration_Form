const loginSchema = Yup.object().shape({
  email: Yup.string()
    .min(5, 'Too Short!')
    .max(50, 'Too Long!')
    .email()
    .label("E-mail")
    .required(),
  password: Yup.string()
    .min(6, 'Too Short!')
    .max(15, 'Too Long!')
    .label("Password")
    .matches(/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[a-zA-Z\d]{6,12}$/, 'Minimum eight characters, at least one uppercase letter, one lowercase letter and one number.')
    .required(),
  confirmPassword: Yup.string()
    .oneOf([Yup.ref('password'), null], 'Passwords must match')
});

const RegisterForm = () => {
  const dispatch = useDispatch();
  let navigate = useNavigate();

  const formik = useFormik({
    initialValues: {
      email: '',
      password: '',
      confirmPassword: '',
    },
    validationSchema: loginSchema,
    onSubmit: values => {
      dispatch(registerOperation({ login: values.login || values.email, email: values.email, password: values.password }, navigate));
    },
  });

  const { errors, values, touched, handleChange, handleBlur, handleSubmit, setFieldValue, setFieldError } = formik;

  const customHandleChange = async (e, fieldName) => {
    setFieldValue(fieldName, e.target.value, true);
  };

  useEffect(() => {
    let mounted = true;

    (async () => {
      if (!errors.email && values.email && touched.email) {
        try {
          const { data } = await axiosInstance.post(`/auth/checkEmail`, { email: values.email });
          if (data.found && mounted) {
            setFieldError('email', '*This login is already in use. Please choose another login');
          }
        } catch (error) {
          if (mounted) {
            setFieldError('email', 'E-mail must be a valid email');
          }
        }
      }
    })();

    return () => {
      mounted = false;
    }
  }, [errors.email, values.email, touched.email, setFieldError]);

  return (
    <div className={styles.registerContainer}>

      <h2 className={styles.registerHeader}>Register</h2>
      <span className={styles.registerHeaderUnderText}>Please fill the details below</span>
      <GoogleButton buttonText="Sign up with Google" />
      <div className={styles.registerHeaderUnderContainer}>
        <div />
        <span>Or sign in with e-mail</span>
        <div />
      </div>

      <form onSubmit={handleSubmit}>
        <div className={styles.formikLoginContainer}>
          <input
            className={`${styles.formikFields} + ${styles.formikLogin}`}
            name="email"
            type="text"
            placeholder="E-mail"
            onChange={e => customHandleChange(e, 'email')}
            onBlur={handleBlur}
            value={formik.values.email}
            autoComplete="off"
          />
          <svg className={styles.formikLoginSvg}>
            <use href={`${svg}#iconLoginSvg`}></use>
          </svg>
          {formik.touched.email && formik.errors.email ? (
            <div className={styles.formikErrorContainer}>
              <span>
                <svg>
                  <use href={`${svg}#iconCrossSvg`}></use>
                </svg>
              </span>
              <p>
                {formik.errors.email}
              </p>
            </div>
          ) : null}
        </div>

        <div className={styles.formikPasswordContainer}>
          <input
            autocomplete="off"
            className={`${styles.formikFields} + ${styles.formikPassword}`}
            name="password"
            type="password"
            placeholder="Password"
            onChange={handleChange}
            onBlur={handleBlur}
            value={formik.values.password}
          />
          <svg className={styles.formikPasswordSvg}>
            <use href={`${svg}#iconPasswordSvg`}></use>
          </svg>
          {formik.touched.password && formik.errors.password ? (
            <div className={styles.formikErrorContainer}>
              <span>
                <svg>
                  <use href={`${svg}#iconCrossSvg`}></use>
                </svg>
              </span>
              <p>
                {formik.errors.password}
              </p>
            </div>
          ) : null}
          {!formik.errors.password &&
          !formik.errors.confirmPassword &&
          formik.touched.password &&
          formik.touched.confirmPassword ? (
            <div className={`${styles.formikErrorContainer} + ${styles.formikErrorContainerToGreen}`}>
              <span>
                <svg>
                  <use href={`${svg}#iconChekSvg`}></use>
                </svg>
              </span>
              <p>
                {formik.errors.confirmPassword}
              </p>
            </div>
          ) : null}
        </div>

        <div className={styles.formikPasswordContainer}>
          <input
            autoComplete="off"
            className={`${styles.formikFields} + ${styles.formikPassword}`}
            name="confirmPassword"
            type="password"
            placeholder="Confirm Password"
            onChange={handleChange}
            onBlur={handleBlur}
            value={formik.values.confirmPassword}
          />
          <svg className={styles.formikPasswordSvg}>
            <use href={`${svg}#iconPasswordSvg`}></use>
          </svg>
          {formik.touched.confirmPassword && formik.errors.confirmPassword ? (
            <div className={styles.formikErrorContainer}>
              <span>
                <svg>
                  <use href={`${svg}#iconCrossSvg`}></use>
                </svg>
              </span>
              <p>
                {formik.errors.confirmPassword}
              </p>
            </div>
          ) : null}

          {!formik.errors.password &&
          !formik.errors.confirmPassword &&
          formik.touched.confirmPassword &&
          formik.touched.password ? (
            <div className={`${styles.formikErrorContainer} + ${styles.formikErrorContainerToGreen}`}>
              <span>
                <svg>
                  <use href={`${svg}#iconChekSvg`}></use>
                </svg>
              </span>
              <p>
                {formik.errors.confirmPassword}
              </p>
            </div>
          ) : null}
        </div>

        <div className={styles.formikButtonContainer}>
          <button className={styles.formikButton} type="submit">Register</button>
          <div className={styles.formikTextContainer}>
            <span>
              Already a member?
            </span>
            <Link to="/login">
              Sign in
            </Link>
          </div>
        </div>

      </form>

    </div>
  );
};
