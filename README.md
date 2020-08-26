# Baltimore-Crime-Prediction
Baltimore Police Department's Crime Dataset (1957-2020)

def plot_trend_data(ax, name, series):
    ax.plot(series.index, series, linewidth=6)
    ax.set_title(f"Baltimore Crime Trend for {name}")
#     ax.set_ylim((0, 2))

def make_design_matrix(arr):
    """Construct a design matrix from a numpy array, converting to a 2-d array
    and including an intercept term."""
    return sm.add_constant(arr.reshape(-1, 1), prepend=False)

def fit_linear_trend(series):
    """Fit a linear trend to a time series.  Return the fit trend as a numpy array."""
    X = make_design_matrix(np.arange(len(series)) + 1)
    linear_trend_ols = sm.OLS(series.values, X).fit()
    linear_trend = linear_trend_ols.predict(X)
    return linear_trend

def plot_linear_trend(ax, name, series):
    linear_trend = fit_linear_trend(series)
    plot_trend_data(ax, name, series)
#     df2['RAPE'].groupby(df2['WEEK']).mean()
    ax.plot(series.index, linear_trend)


# ax.set_facecolor('w')
fig, ax = plt.subplots(1, figsize=(40, 25))
plt.rc('font', size=SMALL)
plt.rc('axes', titlesize=BIGGER)     
plt.rc('axes', labelsize=BIGGER)   
plt.rc('xtick', labelsize=MEDIUM)
plt.rc('ytick', labelsize=MEDIUM)    
plt.rc('legend', fontsize=SMALL)
plt.rc('lines', linewidth=4)
ax.set_xlabel('Week', labelpad=60, horizontalalignment='center')
plot_linear_trend(ax, 'Shootings', df2['SHOOTING'].groupby(df2['WEEK']).mean())
plt.tight_layout()

